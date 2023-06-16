---
title: "【Next.js】Firebase Analytics is not supported in this environment"
emoji: "⚠️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Next", "Firebase", "Analytics"]
published: true
---

# 【Next.js】Firebase Analytics is not supported in this environment.

## Wrap initialization of analytics in analytics.isSupported()
```
analytics.isSupported()
```
を用いて、Firebase Analyticsを使えるか確認してから呼び出してねということらしい！
[Analytics: problem with "prevent initialization in unsupported environments" handling ](https://github.com/firebase/firebase-js-sdk/issues/3573)


## Firebase Analyticsが使えない状態がありうる
今回はNext.jsを使っていますが、Firebase Analyticsに限らず呼び出だしタイミングが結構難しかったです。
Next.js 13ではappディレクトリを使う実装とそうでないものがありますが、従来の getStaticProps や getServerSidePropsが使えません。
なので環境に応じて呼び出すタイミングを考慮する必要があります。具体的にいうとサーバー上でレンダリングされるタイミングでも問題ないようにしてあげないといけません。

私は以下のように実装していて怒られました。
```
// 変更前
import { getAnalytics } from "firebase/analytics";
const analytics = getAnalytics(app);
```

## isSupportedを使って使っていいか確認
isSupportedメソッドで使っていいかを確認し、使えないようなら予め用意したMockを使って、エラーにならないようにします。

```
// 変更後
import { getAnalytics, isSupported } from "firebase/analytics";
const analyticsMock = {
    logEvent: () => {},
    setCurrentScreen: () => {},
    setUserId: () => {},
}
const analytics = isSupported() ? getAnalytics(app) : analyticsMock;
```

## まとめ
慣れるまではタイミングが難しい！！！