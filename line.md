# LINE ミニアプリ

[LINEミニアプリ](https://developers.line.biz/ja/services/line-mini-app/)についての調査メモです。

[LINEミニアプリとは](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/)

> LINEミニアプリは、[LIFF（LINE Front-end Framework）](https://developers.line.biz/ja/docs/liff/)上で実行されるウェブアプリです。LINEミニアプリを使えば、ユーザーはアプリをインストールしなくてもサービスを利用できます。
> LINEミニアプリはウェブアプリですので、HTML5のほとんどの仕様が使用できます。詳しくは、「[仕様](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)」を参照してください。

> LINEミニアプリは[LINEミニアプリポリシー (opens new window)](https://terms2.line.me/LINE_MINI_App?lang=ja)における「本サービスのご利用対象者」であれば、どなたでも開発することができます。

> 本サービスのご利用対象者
> - 日本の法人番号、または台湾やタイの納税番号がある組織
> - 日本の個人事業主

## 1 開発前の調査メモ

### 1-1 [仕様](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)

> LINEミニアプリは、[LIFFアプリ](https://developers.line.biz/ja/docs/liff/overview/)の一種です。そのため、LINEミニアプリの対応するOSバージョンとLINEバージョンは、LIFFの推奨環境に準拠しています。

#### 1-1-1 推奨環境

- iOS：最新バージョン。WKWebViewが使用されます。
- Android：最新バージョン。Android WebViewが使用されます。
- LINE：最新バージョン

>  LIFFアプリは、OS、LINEともに最新バージョンの環境での利用を推奨します

#### 1-1-2 HTML5サポート

> LINEミニアプリを開発する場合は、HTML5のほとんどの仕様を使用できます。たとえば、Geolocation APIを使用して、ユーザーの位置情報を取得し、近くの店舗の情報をユーザーに提供できます。Google Maps APIなど、HTML5と互換性のあるほとんどのMap APIも使用できます。

#### 1-1-3 LINEミニアプリの構造

[LINEミニアプリの構造](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/#what-does-line-mini-app-look-like)

> LINEミニアプリのページは、（A）ヘッダーおよび（B）ボディで構成されています。詳しくは、「[LINEミニアプリの構造](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/)」を参照してください。

![LINEミニアプリの構造](https://developers.line.biz/assets/img/mini_concept.47451080.png)

##### 1-1-3-1 ヘッダー

> LINEミニアプリのヘッダーは、プラットフォームネイティブのコンポーネントが使用されており、LINEが自動生成します。ヘッダーは、以下のコンポーネントで構成されています。

1. サービス名
    - LINEミニアプリのページで指定した`<title>`要素が表示されます。フォントは設定できません。
2. アクションボタン
    - タップすると、ユーザーがLINEミニアプリのページを友だちとシェアしたり、ユーザーのKeepに保存したり、ページをリロードするためのオプションが表示されます。オプションのテキストは設定できません。
3. 閉じるボタン
    - LINEミニアプリを閉じます。
4. 戻るボタン
    - 前のページを表示します。
5. ローディングバー
    - 現在のページの読み込み状況を表示します。

![LINEミニアプリのヘッダー](https://developers.line.biz/assets/img/mini_uicomp_header.f3ca54a7.png)

> ヘッダーでは、標準で以下の色が使用されます。
> 背景：白
> テキストおよびボタンのラベル：黒
> ヘッダーの背景色をブランドカラーに変更できます。 LINE Developersコンソールの［LIFF］タブで、「ヘッダー背景色」に16進数カラーコード（例：#00c300）を入力してください。

##### 1-1-3-2 ボディ

> ボディはWebViewが使用されています。HTML5およびLIFFを活用して、サービスごとに開発してください

#### 1-1-4 LINEミニアプリの機能

##### 1-1-4-1 ビルトイン機能

- アクションボタン
    - シェア
        - 現在開いているページをLINEメッセージでシェアします。
    - 閲覧中のページを最小化
        - [LIFFブラウザを最小化](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/)します。
    - サービス提供元の詳細を見る
        - [プロバイダーページ](https://developers.line.biz/ja/docs/partner-docs/provider-page/)を表示します。
    - 更新
        - 現在開いているページを再読み込みします。
- チャンネル同意画面
    - チャネル同意画面は、ユーザーが初めてLINEミニアプリを利用するときに表示されます。チャネル同意画面では、LINEミニアプリごとにアクセス権限を付与するかどうかをユーザーに確認します。
    - すべてのLINEミニアプリはデフォルトで以下の権限を要求します。
        - ユーザーのプロフィール情報を取得する権限
        - トークへのメッセージを送信する権限
    - チャネル同意画面では、LINEヤフー株式会社によって承認された権限のみを、ユーザーに要求できます。 LINE DevelopersコンソールのLINEミニアプリチャネルの設定で、ユーザーに権限を要求する項目を指定できます。

##### 1-1-4-2 カスタム機能

- サービスメッセージ
    - サービスメッセージは、ユーザーからのリクエストに対する確認や応答としてユーザーが知るべき情報を、LINEミニアプリから通知する機能です。
    - [サービスメッセージを送信する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)
    - [サービスメッセージの条件](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/#conditions-for-service-messages)
- ユーザーをLINE公式アカウントの友だち追加へ誘導する
    - LINEミニアプリでは、友だち追加オプションを使って、チャネル同意画面、もしくはアクセス許可要求画面からLINE公式アカウントの友だち追加への誘導ができます。
    - [LINEミニアプリをはじめて開いたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/#link-a-line-official-account-with-your-channel)
- 決済システムの利用
    - LINE Payだけでなく、クレジットカードなどの支払い方法をLINEミニアプリに統合できます。
    - [決済システムを利用する](https://developers.line.biz/ja/docs/line-mini-app/develop/payment/)
- [カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)
- [LINE Profile+](https://developers.line.biz/ja/docs/partner-docs/line-profile-plus/)
    - LINEミニアプリでは、名前、性別、生年月日、電話番号、住所などのユーザー情報を取得してサービスに利用することができます。
    - この機能は、所定の申請等を行った法人ユーザーのみが利用可能です。

##### 1-1-4-3 LIFFアプリにできてLINEミニアプリでできないこと

- 外部ブラウザによる表示
    - 外部ブラウザでLINEミニアプリを開くとLINEミニアプリをスマートフォン版LINE（LIFFブラウザ）で開くように案内されます。
- アクションボタンの非表示（モジュールモード）
    - LINEミニアプリでは、[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を非表示にすることはできません。LINEミニアプリチャネルに追加されているLIFFアプリでは、［モジュールモード］は設定できません。

#### 1-1-5 [パフォーマンスガイドライン](https://developers.line.biz/ja/docs/line-mini-app/develop/performance-guidelines/)

> LINEヤフー株式会社では、以下のスコアを満たすことを推奨しています。

| パフォーマンス計測ツール | スコア |
| ---- | ---- |
| [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) | Performance: 50以上 |

> - LINEログインが実行されない状態で計測してください。LINEログインが実行されると、LINEログインのページのパフォーマンスが計測され、LINEミニアプリのパフォーマンスは計測されません。
> - プロダクション環境（本番環境）で計測してください。スコアは、ネットワーク環境などの影響を受ける場合があります。

#### 1-1-6 [開発ガイドライン](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/)

> LINEミニアプリを使ったウェブアプリを開発する際は、以下の開発ガイドラインに従ってください。
> - LINEプラットフォームへの大量リクエストの禁止
> - ログ保存の推奨
> LINEミニアプリはLIFFで提供される仕組みを利用しています。そのため、『LIFFドキュメント』の「[LIFFアプリ開発ガイドライン](https://developers.line.biz/ja/docs/liff/development-guidelines/)」の内容にも従ってください。
> LINEミニアプリ開発における基本ルールは、[規約とポリシー](https://developers.line.biz/ja/terms-and-policies/)に記載される内容に基づきます。

##### 1-1-6-1 [LINEプラットフォームへの大量リクエストの禁止](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#prohibiting-mass-requests-to-line-platform)

> 負荷テストを目的に、LIFF URLスキーム （https://liff.line.me/{liffId}）を経由してLINEミニアプリへ大量のアクセスを行ったり、LIFF APIやサービスメッセージAPIに大量のリクエストを送信したりしないでください。LINEミニアプリの負荷テストを行う場合は、LINEプラットフォームへの大量のリクエストが発生しないテスト環境を用意してください。
> レート制限を超えて送信を行った場合、429 Too Many Requestsが返却され、エラーとなります。

##### 1-1-6-2 [ログ保存の推奨](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#liff-development-rules3)

> 問題が発生した際に、開発者自身が原因や影響範囲の調査を円滑に行えるよう、[サービスメッセージAPIのリクエスト](https://developers.line.biz/ja/reference/line-mini-app/)のログを一定期間保存することを推奨します。

###### 1-1-6-2-1 [サービスメッセージAPIリクエスト時のログ](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#service-message-API-request-logs)

> [サービスメッセージAPI](https://developers.line.biz/ja/reference/line-mini-app/)のリクエストを行った際は、レスポンスに含まれる、[サービス通知トークン](https://developers.line.biz/ja/reference/line-mini-app/#issue-notification-token-response)`notificationToken`に加え、以下の情報をログとして保存することを推奨します。
> - APIリクエストを行った時間
> - リクエストメソッド
> - APIエンドポイント
> - LINEプラットフォームからレスポンスされたステータスコード

| APIリクエストを行った時間 | リクエストメソッド | APIエンドポイント | ステータスコード|
| ---- | ---- | ---- | ---- |
| Mon, 16 Jul 2021 10:20:23 GMT | POST | https://api.line.me/message/v3/notifier/send?target=service | 200 |

> 運用するLINEミニアプリの要件等によっては、上記に加えて、たとえば以下のような情報を保存しておくことで、問題が発生した際の調査をより円滑に行うことができます。
> - サービスメッセージAPIに対するリクエストのボディ
> - APIリクエスト後にLINEプラットフォームから返却されたサービス通知トークン`notificationToken`以外のレスポンスのボディ

> サービスメッセージAPIのリクエストのログ等は、お問い合わせいただいても提供は行っておりません。ログの保存は、LINEミニアプリを開発する開発者自身で行ってください。

##### 1-1-6-3 [LIFFアプリ開発ガイドライン](https://developers.line.biz/ja/docs/liff/development-guidelines/)

##### 1-1-6-3-1 [ユーザー情報は必ず安全に取り扱う](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules1)
> LIFFアプリおよびサーバーでユーザー情報を使用する場合、LIFFアプリでユーザー情報を正しく処理しないと、なりすましやその他の種類の攻撃に対して脆弱になります。LIFFアプリおよびサーバーで、LIFFアプリで取得したユーザー情報を、安全に使用する方法について詳しくは、「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。
> LIFFのエンドポイントURLやLIFF URLのURLフラグメントには、アクセストークンやユーザーIDなどの機密情報が含まれます。外部にURLが漏洩しないように注意してください。

###### 1-1-6-3-1-1 [LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」

> ユーザーが、LIFFブラウザでLIFFアプリを起動したり、外部ブラウザでLIFFアプリを起動してliff.initメソッドでログイン処理を行ったりすると、LIFFアプリはユーザーのプロフィール（ユーザーID、表示名、プロフィール画像、メールアドレス）を取得できます。
> LIFFアプリで、これらのユーザー情報を正しく処理しないと、なりすましやその他の種類の攻撃に対して脆弱になります。
> このページでは、LIFFアプリを開いたユーザーのユーザー情報を、LIFFアプリおよびサーバーで安全に使用する方法を説明します。

- ユーザー情報をサーバーで使用する場合は、IDトークンまたはアクセストークンを、LIFFアプリからサーバーに送信してください。サーバーは、LIFFアプリが送信したトークンを、さらにLINEプラットフォームに送信することで、ユーザーのプロフィールを安全に取得できます。
    - IDトークンを送信してユーザー情報を取得する
        - [liff.getIDToken()](https://developers.line.biz/ja/reference/liff/#get-id-token)で取得したIDトークンをサーバーに送信した場合は、サーバーでIDトークンを検証する（[POST /oauth2/v2.1/verify](https://developers.line.biz/ja/reference/line-login/#verify-id-token)）ことで、ユーザーのプロフィール情報を安全に取得できます。
    - アクセストークンを送信してユーザー情報を取得する
        - [liff.getAccessToken()](https://developers.line.biz/ja/reference/liff/#get-access-token)で取得したアクセストークンをサーバーに送信した場合は、サーバーでアクセストークンの有効性を検証し（[GET /oauth2/v2.1/verify](https://developers.line.biz/ja/reference/line-login/#verify-access-token)）、さらにチャネルIDとアクセストークンの有効期限を検証することで、ユーザーのプロフィール情報を安全に取得できます（[GET /v2/profile](https://developers.line.biz/ja/reference/line-login/#get-user-profile)）。
        - ユーザーがLIFFアプリを閉じると、有効期限が切れていなくてもアクセストークンは無効化されます。
    - ユーザー情報をLIFFアプリで使用する
        - [liff.getDecodedIDToken()](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)または[liff.getProfile()](https://developers.line.biz/ja/reference/liff/#get-profile)で取得したユーザーのプロフィール情報を使用してください。
- liff.getDecodedIDToken()およびliff.getProfile()で取得したユーザーのプロフィールの詳細を、LIFFアプリからサーバーに送信しないでください。
- LIFF SDKは、LINEプラットフォームから取得したIDトークンおよびアクセストークンを検証しています。そのため、liff.getIDToken()およびliff.getAccessToken()で取得したトークンは信用できます。

###### 1-1-6-3-1-2 [LIFFアプリを初期化する際の注意点](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules2)

> liff.init()メソッドが返すPromiseオブジェクトがresolveする前に、サーバーやフロントエンド側の処理などでURLを変更しないようにしてください。URLを変更すると、INIT_FAILEDが返され、LIFFアプリを開けません。 そのほか、LIFFアプリ初期化時の注意事項について詳しくは、「[LIFFアプリを初期化する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app)」を参照してください。

###### 1-1-6-3-1-3 [LIFFアプリを開発する際に必ず守るべきこと](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules3)

- LIFFアプリをSPA（Single Page Application）で構築する場合、LIFFはフラグメントを用いたルーティングとは相性が悪いため、[History API](https://html.spec.whatwg.org/multipage/nav-history-apis.html#the-history-interface)を利用して実装してください。
- 以下のようなデバイスまたはOSの機能を利用するAPIは、必ずユーザー操作をきっかけにして実行されるように実装してください。
    - 位置情報の取得
    - カメラへのアクセス
    - マイクへのアクセス
- ユーザーの同意なく、cookie、localStorage、またはsessionStorageを使ってユーザーをトラックしたり、LINEのユーザー情報と外部セッション情報を結びつけたりしないでください。
- テスト段階のLIFFアプリに対するアクセス権限は、LIFFアプリ側で制限してください。
- LIFFアプリとLIFFアプリ内で開くコンテンツのURLスキームは、httpsである必要があります。コンテンツのURLスキームがhttpの場合は、[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)で表示されます。この場合、LIFFアプリとしてチャネルに追加されていても、LIFFアプリとして動作しません。
- LIFFアプリではcookie、localStorage、またはsessionStorageを利用できます。ただし、OSの仕様変更によって将来的に利用が制限される可能性があります。

###### 1-1-6-3-1-4 [LINEプラットフォームへの大量リクエストの禁止](https://developers.line.biz/ja/docs/liff/development-guidelines/#prohibiting-mass-requests-to-line-platform)

> 負荷テストを目的に、[LIFF URLスキーム](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/#opening-a-liff-app) （https://liff.line.me/{liffId}）を経由してLIFFアプリへ大量のアクセスを行ったり、[LIFF API](https://developers.line.biz/ja/reference/liff/)に大量のリクエストを送信したりしないでください。LIFFアプリの負荷テストを行う場合は、LINEプラットフォームへの大量のリクエストが発生しないテスト環境を用意してください。

> レート制限を超えて送信を行った場合、429 Too Many Requestsが返却され、エラーとなります。

### 1-2 デザイン

#### 1-2-1 [LINEミニアプリのアイコン](https://developers.line.biz/ja/docs/line-mini-app/design/line-mini-app-icon/)

##### 1-2-1-1 アイコンのサイズ

> アイコンの背景領域（BG SIZE）のサイズは、130x130pxにしてください。

##### 1-2-1-2 ロゴのサイズ

> ロゴのサイズ（LOGO SIZE）は、最小で54x54px、最大で90x90pxにしてください。なお、54x54pxから76x76pxにすることを推奨します。

##### 1-2-1-3 ロゴのデザイン

> ロゴの視認性と品質を常に保つために、ロゴは単独のシンボルまたはワードマークとしてデザインしてください。

##### 1-2-1-4 アイコンのフォーマット

> アイコンとして利用可能なファイルフォーマットは、PNGとJPEGのみです。

##### 1-2-1-4 アイコン用の画像をアップロードする方法

> LINE Developersコンソールの［チャネル基本設定］タブにある［チャネルアイコン］より、アイコン用の画像をアップロードします。

##### 1-2-1-5 [アイコンのテンプレート](https://developers.line.biz/ja/docs/line-mini-app/design/line-mini-app-icon/#icon-color)

> アイコンの作成に利用できるPSD形式のテンプレートファイルを提供しています。テンプレートファイルを用いることで、アイコンのアウトラインを設定できます。アウトラインを設定することで、LINEアプリ上でアイコンと同系色の背景の前面にアイコンが掲載された場合でも、アイコンを認識しやすくなります。

[アイコンのテンプレート](https://vos.line-scdn.net/line-developers/docs/media/line-mini/icon_template_file.psd)

> テンプレートファイルをもとにアイコンを作成する際は、背景領域の色（Background color）に応じて、輪郭色（Outline Color）を指定してください。このとき、テンプレートファイルにおいて、背景色のタイプを選択することを推奨します。また、テンプレートファイルの未使用のレイヤーは非表示にした上で保存してください。

#### 1-2-2 [LINEミニアプリのセーフエリア](https://developers.line.biz/ja/docs/line-mini-app/design/landscape/)

> ノッチがある端末でもLINEミニアプリのすべてを表示するために、CSSを使ってLINEミニアプリをセーフエリアに収めることを推奨します。 LINEミニアプリでは、ノーマルモードとランドスケープモードの両方をサポートします。ノーマルモードとランドスケープモードでは、必要なセーフエリアが異なります。

##### 1-2-2-1 ノーマルモード

- 下：34px

```css
{
    padding-bottom: 34px;
}
```

##### 1-2-2-2 ランドスケープモード

- 左右：44px
- 下：34px

```css
{
    padding-right: 44px;
    padding-bottom: 21px;
    padding-left: 44px;
}
```

#### 1-2-3 [読み込み中アイコン](https://developers.line.biz/ja/docs/line-mini-app/design/loading-icon/)

> 読み込み中アイコンは、LINEミニアプリで推奨されているUI要素です。
> 以下のスピナー（svgファイル）をダウンロードして、読み込み中アイコンとして使用してください。 
> - ライトモード用スピナー（[Download](https://developers.line.biz/media/line-mini-app/LINE_spinner_light.svg)）
> - ダークモード用スピナー（[Download](https://developers.line.biz/media/line-mini-app/LINE_spinner_dark.svg)）
> スピナーのサイズは、30x30ピクセルです。 スピナーは、画面中央に表示してください。

### 1-3 運用

#### 1-3-1 公開

##### 1-3-1-1 [LINEミニアプリポリシー](https://terms2.line.me/LINE_MINI_App?lang=ja)

##### 1-3-1-2 [審査を依頼する](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)

##### 1-3-1-2-1 [審査依頼前の確認事項](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)

- LINEミニアプリが、すべてのガイドラインやルールに従っていること。
特に、以下のガイドラインおよびルールを確認してください。
    - [LINEミニアプリのアイコンを作成する](https://developers.line.biz/ja/docs/line-mini-app/design/line-mini-app-icon/)
    - [ランドスケープモードのセーフエリア](https://developers.line.biz/ja/docs/line-mini-app/design/landscape/)
    - [読み込み中アイコン](https://developers.line.biz/ja/docs/line-mini-app/design/loading-icon/)
    - [カスタムアクションボタンを実装する](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)
    - [パフォーマンスガイドライン](https://developers.line.biz/ja/docs/line-mini-app/develop/performance-guidelines/)
- LINEミニアプリが、「[LINEミニアプリポリシー (opens new window)](https://terms2.line.me/LINE_MINI_App?lang=ja)」を遵守していること
- [LINE Developersコンソール](https://developers.line.biz/console/)でLINEミニアプリチャネルに登録した情報が、正しく、最新であること。
    - プロバイダー名は、「サービス提供者」と同一であること。
    - 「[チャネル説明](https://developers.line.biz/ja/docs/line-mini-app/discover/console-guide/#channel-description)」に、正しいサービス内容が記載されていること。
    - プライバシーポリシーでは、ユーザー情報を取得する会社をプロバイダー名と同じ会社に設定する必要 があります。
- 本番用のチャネルのLIFF URLと、審査用のチャネルのLIFF URLが同じサービスを反映しているかどうかを確認してください。
    - 審査時、LINEヤフー株式会社は審査用のチャネルのLIFF URLを確認します。チャネルやLIFF内の各種設定は自動的に審査用のチャネルへコピーされ、提供されます。ただし、審査用チャネルのLIFF URLが本番用のチャネルのLIFF URLと同じサービス内容を提供しているか、念のために事前確認してください。

##### 1-3-1-2-2 [審査のプロセス](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)

1. LINE Developersコンソールの［ワークフロー］タブで必要な情報を入力して、審査を依頼します。
    - 審査対象のLINEミニアプリにベーシック認証によるアクセス制限をかけている場合は、審査を依頼する際に［ワークフロー］タブの［審査のための補足資料］でユーザー名とパスワードをお知らせください。詳しくは、「[公開前のLINEミニアプリにベーシック認証でアクセス制限をかける](https://developers.line.biz/ja/docs/line-mini-app/develop/develop-overview/#use-basic-authentication)」を参照してください。
    - 審査は、LINE Developersコンソールの［チャネル基本設定］タブにある［チャネル説明］に記載された内容をもとに行われます。このため、以下の例を参考に、正しいサービス内容を記載してください。
        - ［チャネル説明］について詳しくは、「[チャネル説明](https://developers.line.biz/ja/docs/line-mini-app/discover/console-guide/#channel-description)」を参照してください。
    - 審査が終了するまでに、1～2週間程度かかります。却下された場合、再申請と再審査にはさらに数日かかります。審査の完了日は事前に指定することはできません。
    - 審査依頼後、審査が始まる前であれば、［ワークフロー］タブの［審査申請をキャンセルする］ボタンからキャンセルできます。
    - 審査を開始したら、審査依頼をキャンセルしたり、入力した情報を変更したりできません。
    - 審査が開始されてステータスが「審査中」になると、審査用チャネルのLIFF URLにアクセスできます。
    - LINE Developersコンソールの［チャネル基本設定］タブの［サービスを提供する地域］に「日本」が設定されている場合、LINEミニアプリチャネルが審査を通過すると、そのプロバイダーは[認証プロバイダー](https://developers.line.biz/ja/docs/line-developers-console/overview/#certified-provider)になります。
        - 認証プロバイダーになると、ユーザーが確認する同意画面に、認証プロバイダーバッジを表示できます。またプロバイダーページを設定、公開できます。
        - 認証プロバイダーバッジは、プロバイダーを作成したサービス提供者が本物であることをLINEヤフー株式会社が確認した証です。
            - 実在している組織であること
            - その組織に所属している人（またはその代理人）からの申請であること
            - プライバシーポリシーを定め、公開している組織であること
        - 認証プロバイダーバッジは、所定の申請等を行った法人ユーザーのみが表示できます。認証プロバイダーバッジを表示したいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/line/)にお問い合わせください。
2. LINEミニアプリの検索を有効にします。
    - LINEミニアプリが承認されると、チャネルのステータスが自動的に「承認済み」になった後、すぐに「公開中」になります。LINE Developersコンソールの［ワークフロー］タブにある［検索可能にする］ボタンを使うと、LINE内でLINEミニアプリを検索できる状態にして、サービスを提供開始できます。
    - 「公開中」になると、LIFF URLが有効になるため、ユーザーがLINEミニアプリにアクセスすることが技術的には可能となります。ただし、LINE内での検索がまだ有効になっていないため、ユーザーがサービスを検索して見つけることはできません。
    - 検索を可能にしたいタイミングで［検索可能にする］ボタンを押すことで、LINE内でLINEミニアプリの検索が可能になります。ただし、ステータスが「公開中」になってから30日以内（土日祝日を含む）に手動で検索可能にしなかった場合は、31日目の午前9:00（JST）に自動的に検索可能となります。
    - LINEミニアプリの検索が有効になると、LINEミニアプリチャネルのステータスは「開発中」に戻り、設定の変更や審査の再申請が改めて可能になります。このとき、設定を変更しても、再度審査を通過して［変更内容を公開する］ボタンを押すまでは、公開中のLINEミニアプリに影響はありません。
3. すでに公開中のLINEミニアプリの場合は、作業の流れが少し異なります。
    - INEミニアプリが承認されると、チャネルのステータスが「承認済み」に変わります。LINE Developersコンソールの［ワークフロー］タブにある［変更内容を公開する］ボタンを使って、手動でチャネルのステータスを「公開中」に変更する必要があります。
    - ステータスが「公開中」になると、審査をリクエストした際に行った変更が、公開中のチャネルおよびそのチャネルのLIFF（LINEミニアプリ名、チャネル設定、LIFF設定など）に反映されます。
    - 公開したいタイミングで［変更内容を公開する］ボタンを押すことで、ステータスが即時に「公開中」になります。ただし、ステータスが「承認済み」になってから30日以内（土日祝日を含む）に手動で変更内容の公開を行わなかった場合は、31日目の午前9:00（JST）に自動的に公開されます。
    - 新しい変更が公開されると、LINEミニアプリチャネルのステータスは「開発中」に戻り、設定の変更や審査の再申請が改めて可能になります。このとき、設定を変更しても、再度審査を通過して［変更内容を公開する］ボタンを押すまでは、公開中のLINEミニアプリに影響はありません。

#### 1-3-2 ユーザーがLINEミニアプリにアクセスする方法

> ユーザーは、LINEからだけでなく、LINE外部からもLINEミニアプリにアクセスできます。LINE内には、LINEミニアプリにアクセスするためのポイントがいくつも用意されています。

##### 1-3-2-1 LINE外部からアクセスする

> [LINEミニアプリのパーマネントリンク](https://developers.line.biz/ja/docs/line-mini-app/develop/permanent-links/)にアクセスすると、LINE外部からもLINEミニアプリにアクセスできます。

LINEミニアプリページのURLに対応するパーマネントリンクの例

```
https://liff.line.me/123456-abcedfg/shop?search=shoes#item10
```

> ユーザーがLINEをインストールしている場合は、ユーザーがパーマネントリンクをクリックすると、LINEが自動的に起動してLINEミニアプリのページが表示されます。 ユーザがLINEをインストールしていない場合は、ウェブブラウザが開き、LINEのダウンロードを求めるページが開きます。ユーザーがLINEをインストールすると、LINEミニアプリを利用できます。

> LINE公式アカウントからもLINEミニアプリにアクセスできます。たとえば、LINE公式アカウントの友だちに送信するリッチメッセージや、LINE公式アカウントとのトーク画面に表示されるリッチメニューに、LINEミニアプリを開くリンクを追加できます。詳しくは、[LINE公式アカウントを活用する](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/#add-a-line-mini-app-shortcut-to-the-rich-menu)を参照してください。

##### 1-3-2-2 LINEで探すからアクセスする

> INEの検索機能からも、LINEミニアプリにアクセスできます。

##### 1-3-2-3 LINEメッセージからアクセスする

> 友だち同士で、LINEミニアプリを簡単にシェアできます。[ビルトインのアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を使用するだけでなく、[カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)を使用して、LINEミニアプリのページをLINEメッセージでシェアできます。

#### 1-3-2 運営ガイド

- [サービス事業主のためのノウハウ](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/)
- [LINEミニアプリ更新後の再審査](https://developers.line.biz/ja/docs/line-mini-app/service/update-service/)
- [LINE公式アカウントを活用する](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/)

## 2 デモアプリを動かす

実際の開発は以下のドキュメントを参照しながら行います。
- [LINEミニアプリ > 開発を始めよう](https://developers.line.biz/ja/docs/line-mini-app/develop/develop-overview/)
- [LINE Front-end Framework (LIFF) > クイックスタート](https://developers.line.biz/ja/docs/liff/)


### 2-1 [実用シナリオ（LINE API Use Case）](https://lineapiusecase.com/ja/usecase.html)

> LINE APIを活用したさまざまな実用シナリオを紹介します。デモアプリやサンプルソースコードを提供しているので、活用方法を具体的にイメージできます。

#### 2-1-1 [LINEで得た顧客の「ID」と「データ」を活かすOMO基盤としてのCDP](https://lineapiusecase.com/ja/usecase/dynamics365.html)

#### 2-1-2 [デジタル時代の新しい購買体験（OMO）をLINEで](https://lineapiusecase.com/ja/usecase/smartretail.html)

##### 2-1-2-1 導入イメージ

![導入イメージ](https://lineapiusecase.com/img/smartretail_PC_image_data.webp)

##### 2-1-2-2 デモ

| OMO型スマートストア | スマホレジ | キャンペーン (友だちへの共有施策) |
| --- | --- | --- |
| ![デモ OMO型スマートストア](https://github.com/ktom1211/memo/assets/83486898/6f9fe812-f465-4ef6-9120-c9fdb2318264) | ![スマホレジ](https://lineapiusecase.com/img/QR_LINE_SmartRetail_ja.webp) | ![キャンペーン (友だちへの共有施策)](https://lineapiusecase.com/img/QR_LINE_SmartRetail_CP_ja.webp) |

##### 2-1-2-3 構成図

![システム図](https://lineapiusecase.com/img/smartretail_system_diagram_azure.webp)
![シーケンス図](https://lineapiusecase.com/img/smartretail_sequence_diagram_azure.webp)

##### 2-1-2-4 サンプルソースコード

- [Azure Serverless版(スマホレジ)](https://github.com/line/line-api-use-case-smart-retail-azure)
- [AWS Serverless版(スマホレジ)](https://github.com/line/line-api-use-case-smart-retail)

### 2-2 リポジトリをクローン

```cmd
git clone https://github.com/line/line-api-use-case-smart-retail-azure.git
```

### 2-3 バージョンを上げる

#### 2-3-1 バックエンド環境の.NETのバージョンを上げる

バックエンドの環境が.Net Core 3.1になっているので、最新の.Net 7に変更する。
アップグレードには[.NET Upgrade Assistant](https://learn.microsoft.com/ja-jp/dotnet/core/porting/upgrade-assistant-overview)を使用した。

1. [.NET Upgrade Assistant](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.upgradeassistant)をインストールする
2. `line-api-use-case-smart-retail-azure\backend\LineApiUseCaseSmartRetail.sln`を開く
3. [src] > [LineApiUseCaseSmartRetail] を右クリック > [upgrade] をクリック
4. [Upgrade Assistant] ウィンドウが開くので、[In-place project upgrade] をクリック
5. 目標のフレームワークを選択して変換を行う
6. [test] > [LineApiUseCaseSmartRetail.test] も同様に実施

`.gitignore`が存在していないのでここでついでに作成する。
 
```powershell
cd backend
dotnet new gitignore
```

#### 2-3-2 フロントエンド環境のNode.jsのバージョンを上げる

Node.js v18.19.0 で動作確認を行う。

1. Node Sass から Dart Sass への移行を行う。

```bash
cd frontend
npm uninstall node-sass
npm install sass
```

2. OpenSSL互換エラーの対応を行う。

Node.js 17以降で導入されたOpenSSL 3.0の変更により、一部の暗号化関連の機能がサポートされなくなったため、そのままではビルドが通らない。
本当はNode.js 18対応のバージョン上げたほうがいいけども（Nuxt 17.2？未検証）、環境変数の設定で対応する。

```bash
npm install --save--dev cross-env
```

```json:pacakge.json
{
  "scripts": {
    "dev": "cross-env NODE_OPTIONS=--openssl-legacy-provider nuxt",
    "build": "cross-env NODE_OPTIONS=--openssl-legacy-provider nuxt build",
    "start": "cross-env NODE_OPTIONS=--openssl-legacy-provider nuxt start",
    "generate": "cross-env NODE_OPTIONS=--openssl-legacy-provider nuxt generate"
  }
}
```

### 2-4 [ラインチャンネルの作成](https://github.com/line/line-api-use-case-smart-retail-azure/blob/main/docs/jp/liff-channel-create.md)

> チャネルは開発者が作成したシステムと LINE プラットフォームの通信を行うための通信路です。 本アプリでは以下の LINE チャネルが必要となるので、手順に従って作成してください。
> - MessagingAPI 用 LINE チャネル
> - LIFF 用 LINE チャネル
> - LINEPay 用 チャネル

#### 2-4-1 プロバイダーの作成

> プロバイダーは複数のチャネルを管理するチーム・会社・個人のようなひとまとまりの単位となります。プロバイダーとチャネルは一対多の関係です。

1. LINE Developes にログインした状態で、以下のコンソールに遷移します。
    - https://developers.line.biz/console/
2. プロバイダー見出しの横にある[作成]ボタンからプロバイダーを作成します。

#### 2-4-2 チャネルの作成

[チャネルを作成する](https://developers.line.biz/ja/docs/liff/getting-started/#step-two-create-channel)

> LINEログイン	LIFFアプリを作成する場合や、次のステップでLIFFスターターアプリを試してみる場合、Create LIFF AppでLIFFアプリの開発環境を構築する場合は、こちらのチャネルを作成してください。
> LINEミニアプリ	LINEミニアプリでLIFFのアプリを作成する場合は、こちらのチャネルを作成してください。

今回はLIFEアプリを試すので、[LINEログイン]を選択する。


[一度作成したチャネルを、後から他のプロバイダーに移動することはできません。](https://developers.line.biz/ja/docs/line-developers-console/overview/#channel-and-provider-linkage)

> 一度作成したチャネルを、後から他のプロバイダーに移動することはできません。
> [LINE Official Account Manager](https://manager.line.biz/)で作成した[LINE公式アカウントでMessaging APIを利用する](https://developers.line.biz/ja/docs/messaging-api/getting-started/#using-oa-manager)際は、初期設定時にチャネルを所属させるプロバイダーを新規作成するか、既存のプロバイダーを選択する必要があります。この場合も、後からチャネルを他のプロバイダーに移動することはできません。
> Messaging APIのチャネルとLINEログインのチャネルを連携するサービスを開発する場合は、これらのチャネルを同じプロバイダーの配下に作成してください。
> 開発者が提供するサービスを利用するLINEユーザーには、プロバイダーごとに異なるユーザーIDが割り当てられます。異なるプロバイダーに属するチャネル間では、ユーザーIDを利用して同一ユーザーであることを確認できません。

##### 2-4-2-1 MessagingAPI 用のチャネルを作成

1. プロバイダーの画面にて、[Messaging API]からチャネルを作成します。
2. 以下の通り、項目を設定します。
    - チャネルの種類： 変更無し
    - プロバイダー： 変更無し
    - 会社・事業者の所在国・地域： 日本
    - チャネルアイコン： 変更無し
    - チャネル名： 任意のチャネル名
        - チャネル名はエンドユーザーが友達追加する際に表示されるアカウント名となります。後から変更可能です。
    - チャネル説明： 任意の説明
    - 大業種： アプリ内容に即した業種
    - 小業種： アプリ内容に即した業種
    - メールアドレス: 変更無し
    - プライバシーポリシー URL： 任意
    - サービス利用規約 URL： 任意
3. [LINE公式アカウント利用規約](https://terms2.line.me/official_account_terms_jp?lang=ja)と[LINE公式アカウントAPI利用規約](https://terms2.line.me/official_account_api_terms_jp?lang=ja)に目を通して同意にチェックを入れます。
4. [作成]をクリックし、チャネルを作成します。

チャネルを作成すると、チャネル名と同名のLINE公式アカウントが作成されます。[LINE Official Account Manager](https://manager.line.biz/)にも、このチャネルに対応するLINE公式アカウントが表示され、各種設定ができるようになります。

[Messaging APIの概要](https://developers.line.biz/ja/docs/messaging-api/overview/#page-title)

##### 2-4-2-2 LIFF 用のチャネルを作成

1. プロバイダーの画面にて、[新規チャンネル作成]から[LINEログイン]を選択します。
2. 以下の通り、項目を設定します。
    - チャネルの種類： 変更無し
    - プロバイダー： 変更無し
    - サービスを提供する地域： 日本
    - 会社・事業者の所在国・地域： 日本
    - チャネルアイコン： 変更無し
    - チャネル名： 任意のチャネル名
        - チャネル名は LINE ログイン時に表示される名称となります。後から変更可能です。
    - チャネル説明： 任意の説明
    - アプリタイプ： ウェブアプリにチェックを入れる
    - 2要素認証の必須化： 任意
        - [2要素認証を必須化する](https://developers.line.biz/ja/docs/line-login/overview/#two-factor-authentication)
    - メールアドレス: 変更無し
    - プライバシーポリシー URL： 任意
    - サービス利用規約 URL： 任意
3. [LINE開発者契約](https://terms2.line.me/LINE_Developers_Agreement?lang=ja)に目を通して同意にチェックを入れます。
4. [作成]をクリックし、チャネルを作成します。

##### 2-4-2-3 [チャネルにLINE公式アカウントをリンクする](https://developers.line.biz/ja/docs/line-login/link-a-bot/#link-a-line-official-account)

1. LINEログインチャンネルの画面にて、［チャネル基本設定］タブをクリックし、［リンクされたLINE公式アカウント］の［編集］をクリックします。
2. ユーザーに友だち追加させるLINE公式アカウントを選択して、［更新］をクリックします。

##### 2-4-2-4 [LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)

1. LINEログインチャンネルの画面にて、［チャネル基本設定］タブをクリックし、[LIFF]のタブに切り替え、[追加]をクリックします。
2. 以下の通り、項目を設定します。
    - LIFF アプリ名： 任意のアプリ名
    - サイズ： Full
        - LINE 内で表示するアプリの縦サイズの設定です。以下リンク参照。後から変更可能です。 https://developers.line.biz/ja/docs/liff/overview/#screen-size
    - エンドポイント URL： https://example.com
        - アプリの作成後、再度設定するので仮の値を入れておきます。
    - Scope: openid, profile にチェック
        - openid：liff.getIDToken()およびliff.getDecodedIDToken()を使用するためのスコープ。
        - profile：liff.getProfile()およびliff.getFriendship()を使用するためのスコープ。
    - [友だち追加オプション](https://developers.line.biz/ja/docs/line-login/link-a-bot/)： On(Aggressive)
        - On (normal)：LIFFアプリの権限の同意画面に、LINE公式アカウントを友だち追加するオプションを追加します。
        - On (aggressive)：LIFFアプリの権限の同意画面の後に、LINE公式アカウントを友だち追加するかどうか確認する画面を表示します。
        - Off：LINE公式アカウントを友だち追加するオプションを表示しません。
    - Scan QR： off
        - このチャネルに追加したLIFFアプリでliff.scanCodeV2()を利用する場合は、オンにします。
    - モジュールモード： off
        - LIFFアプリをモジュールモードで使用する場合は、オンにします。［モジュールモード］をオンにすると、アクションボタンを非表示にできます。このオプションはLIFFアプリの画面サイズで［Full］を選択している場合のみ表示されます。
3. [追加]をクリックし、LIFFアプリを追加します。

##### 2-4-2-5 LINE Pay用のチャネルを作成

> こちらの手順では[LINE Pay Developers](https://pay.line.me/tw/developers/main/main?locale=ja_JP)の[Sandboxを利用したデモ動作](https://pay.line.me/tw/developers/techsupport/sandbox/testflow?locale=ja_JP)用のチャネルを作成します。実際のLINEPayによる課金は行われません。本番環境として利用する場合は、開発者が別途実装をお願い致します。

1. [LINE Pay Developers](https://pay.line.me/tw/developers/main/main?locale=ja_JP)cdにアクセスし、[Sandbox生成](https://pay.line.me/tw/developers/techsupport/sandbox/creation?locale=ja_JP)を行います。
2. 以下の通り、項目を設定します。
    - 国家: JP
    - サービスタイプ: Online
    - 通貨: JPY
    - Emailアドレス: 利用できるアドレスを入力
3. [Submit]をクリックし、Sandboxを生成します。
4. 入力したメールアドレス宛てにLINE Payからメールが来ていることを確認します。
5. [加盟店 My Pageログイン](https://pay.line.me/portal/jp/auth/login)にアクセスし、メールに記載された申請情報（テストIDとパスワード）にて加盟店センターにログインします。
6. [決済連動管理] > [連動キー管理] にて、[照会]をクリックします。
7. メールアドレスに認証コードが送信されるので、入力して[確認]をクリックします。
8. 生成された`Channel ID`と`Channel Secret Key`は後ほどの手順で利用するので控えておきます。
    - この情報は販売者ごとに一意に生成されるため、どこにも公開してはいけません。

### 2-5 [Azure DevOpsを使用してデプロイする](https://github.com/line/line-api-use-case-smart-retail-azure/blob/main/docs/jp/deployment.md)

[Azure Pipeline + Github使ってタダでCI/CDしちゃおう](https://qiita.com/nekia/items/b26f867180e7e8ab7b43)

#### 2-5-1 環境準備

- Azure アカウントの作成
    - [Azure の無料アカウントを今すぐ作成する | Microsoft Azure](https://azure.microsoft.com/ja-jp/free/)
- Azure DevOps アカウントの作成
    - [Azure DevOps にサインアップする](https://learn.microsoft.com/ja-jp/azure/devops/user-guide/sign-up-invite-teammates?view=azure-devops&tabs=microsoft-account)
    - [Azure Pipelinesの無償利用枠の申請](https://aka.ms/azpipelines-parallelism-request)
        - [Azure Pipelines を無料枠で使おうとして躓いた話](https://qiita.com/Hachiyou-Renge/items/2083f2ce9e8b38558805)
- Azure CLI の Bash 環境
    - [Azure Cloud Shell](https://docs.microsoft.com/ja-jp/azure/cloud-shell/quickstart)
        - サブスクリプションの設定
            - `az account set --subscription <サブスクリプションID>`
    - [Azure CLI をローカルインストール](https://learn.microsoft.com/ja-jp/cli/azure/install-azure-cli)
        - インストール
            - `winget install -e --id Microsoft.AzureCLI`
        - Azure CLIにサインイン
            - `az login`
        - サブスクリプションの設定
            - `az account set --subscription <サブスクリプションID>`
- [Azure DevOps CLI](https://learn.microsoft.com/ja-jp/azure/devops/cli/?view=azure-devops)
    - インストール
        - `az extension add --name azure-devops`
    - 組織を設定
        - `az devops configure --defaults organization=https://dev.azure.com/<組織名>/`

#### 2-5-2 Azure リソース作成

Bash on Windows で実行するとパスの形式が異なるため、エラーになる場合がある。その場合は、PowerShell で実行するかAzure Cloud Shellを使用する。

1. Azure リソースを作成します。

```bash
# 任意のグループ名を指定してください。
rg=demo-linesmartretail
az group create -n $rg -l eastasia
az deployment group create -g $rg --template-file main.bicep
```

```powershell
$rg = "demo-linesmartretail"
az group create -n $rg -l eastasia
az deployment group create -g $rg --template-file main.bicep
```

- [リソースグループ名の制限について](https://learn.microsoft.com/ja-jp/archive/blogs/jpaztech/rgname)
- [Azure リソースの名前付けおよびタグ付けの戦略を作成する](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging)
- [名前付けの概要](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/govern/resource-consistency/naming?source=recommendations)
- [リソースの名前付けとタグ付けの意思決定ガイド](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming-and-tagging-decision-guide?source=recommendations)
- [名前付け規則を定義する](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming?source=recommendations)
- [Azureリソースグループとは](https://hyoublog.com/2021/02/05/azure%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B0%E3%83%AB%E3%83%BC%E3%83%97%E3%81%A8%E3%81%AF/)
- [弊社で使っているAzureリソースのスルメ系命名規則を紹介します](https://zenn.dev/aeonpeople/articles/0b4a4be83d0dfd)

2. デプロイトークンを取得します。

```bash
staticAppId=$(az resource list -g $rg --query "[?type=='Microsoft.Web/staticSites'].id" -o tsv)
az rest --method post --url "$staticAppId/listsecrets?api-version=2020-06-01" --query 'properties.apiKey' -o tsv
```

```powershell
$staticAppId = az resource list -g $rg --query "[?type=='Microsoft.Web/staticSites'].id" -o tsv
az rest --method post --url "$($staticAppId)/listsecrets?api-version=2020-06-01" --query 'properties.apiKey' -o tsv
```

以降の手順で利用するため、この値は保存しておいてください。

これらのコマンドは、指定されたリソースグループ内の静的サイトのIDを取得し、そのIDを使用してサイトのAPIキーを取得します。これは、Azure上で静的サイトを管理する際に、プログラム的にAPIキーを取得するために使用されます。

1. `staticAppId=$(az resource list -g $rg --query "[?type=='Microsoft.Web/staticSites'].id" -o tsv)`
    - `az resource list`: Azureリソースのリストを取得します。
    - `-g $rg`: $rg変数に格納されているリソースグループを指定します。
    - `--query "[?type=='Microsoft.Web/staticSites'].id"`: 取得したリソースの中から、タイプがMicrosoft.Web/staticSites（静的サイト）であるもののIDを抽出します。
    - `-o tsv`: 出力をタブ区切りの値（TSV形式）で表示します。
    - `staticAppId=$(...)`: コマンドの結果（静的サイトのID）をstaticAppId変数に格納します。
2. `az rest --method post --url "$staticAppId/listsecrets?api-version=2020-06-01" --query 'properties.apiKey' -o tsv`
    - `az rest`: Azure REST APIにリクエストを送信します。
    - `--method post`: HTTP POSTメソッドを使用します。
    - `--url "$staticAppId/listsecrets?api-version=2020-06-01"`: $staticAppId変数に格納された静的サイトのIDを使用して、そのサイトのシークレット（秘密情報）をリストするAPIエンドポイントにリクエストします。api-version=2020-06-01はAPIのバージョンを指定しています。
    - `--query 'properties.apiKey'`: レスポンスからproperties.apiKey（APIキー）のみを抽出します。
    - `-o tsv`: 出力をタブ区切りの値（TSV形式）で表示します。

3. Azure Static Web Appsのホスト名を取得します。

```bash
az rest --method get --url "$staticAppId?api-version=2020-06-01" --query 'hostNameSslStates[0].hostName' -o tsv
```

```powershell
az rest --method get --url "$($staticAppId)?api-version=2020-06-01" --query 'hostNameSslStates[0].hostName' -o tsv
```

以降の手順で利用するため、この値は保存しておいてください。

このコマンドは、静的サイトのIDを使用してサイトのホスト名を取得します。これは、Azure上で静的サイトを管理する際に、プログラム的にホスト名を取得するために使用されます。

1. `az rest`: Azure REST APIにリクエストを送信します。
2. `--method get`: HTTP GETメソッドを使用します。
3. `--url "$staticAppId?api-version=2020-06-01"`: $staticAppId変数に格納された静的サイトのIDを使用して、そのサイトの情報を取得するAPIエンドポイントにリクエストします。api-version=2020-06-01はAPIのバージョンを指定しています。
4. `--query 'hostNameSslStates[0].hostName'`: レスポンスからhostNameSslStates[0].hostName（ホスト名）のみを抽出します。
5. `-o tsv`: 出力をタブ区切りの値（TSV形式）で表示します。

#### 2-5-3 アプリケーションデプロイ

[Azure DevOps の ビルドパイプラインを CLI で試してみた](https://qiita.com/mnrst/items/1003dcf949c6dddfa8a6)
[Azure Pipelinesのコマンドの基本的な使い方](https://zenn.dev/gekal/articles/azure-devops-pipeline-cli-sample)

1. Azure DevOpsに新しいプロジェクトを作成します。
    - [Azure DevOps にプロジェクトを作成する](https://docs.microsoft.com/ja-jp/azure/devops/organizations/projects/create-project?view=azure-devops&tabs=preview-page)
    - `az devops project create --name <プロジェクト名>`
    - `az devops configure --defaults organization=https://dev.azure.com/<組織名>/project=<プロジェクト名>/`
2. Azure DevOpsに新しいリポジトリを作成します。
    - [Azure Repos にリポジトリを作成する](https://docs.microsoft.com/ja-jp/azure/devops/repos/git/create-new-repo?view=azure-devops&tabs=browser)
    - `az repos create --name <リポジトリ名> --project <プロジェクト名>`
3. リポジトリにコードをプッシュします。
    - `git remote add origin https://<組織名>@dev.azure.com/<組織名>/<プロジェクト名>/_git/<リポジトリ名>`
    - `git push -u origin main`
4. Azure Pipelinesに新しいパイプラインを作成します。
    - [Azure Pipelines にパイプラインを作成する](https://docs.microsoft.com/ja-jp/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=java%2Cyaml%2Cbrowser%2Ctfs-2018-2)
    - `az pipelines create --name <パイプライン名> --repository <リポジトリ名>  --branch main --repository-type tfsgit --yml-path ./azure-pipelines.yml --skip-first-run true`
4. 変数の追加
    - `az pipelines variable create --name deployment_token --value <デプロイトークン> --secret true --pipeline-name=<パイプライン名>`
    - `az pipelines variable create --name LIFF_ID --value <LIFFアプリID> --pipeline-name=<パイプライン名>`
    - `az pipelines variable create --name BASE_HOSTNAME --value <Azure Static Web Appsのホスト名> --pipeline-name=<パイプライン名>`
5. パイプラインの実行
    - `az pipelines run --name <パイプライン名>`

##### 2-5-3-1 ローカルからのデプロイ

Azure Piplinesが無料枠の申請が必要なため、ローカルで実行する場合は以下の手順を実施する。

[Azure Static Web Apps CLI を使用して静的 Web アプリをデプロイする](https://learn.microsoft.com/ja-jp/azure/static-web-apps/static-web-apps-cli-deploy)
[Azure Static Web Apps CLIを使ってローカル開発環境を構築する（2）](https://miyohide.hatenablog.com/entry/2022/12/25/140605)
[NextjsでSSGをしてSWA CLIを使って、Azure Static Web Appsに簡単デプロイ（ローカル上でSSG確認する方法付き）](https://qiita.com/fsdg-takada/items/ff64bc0d46bc2e2a470b)
[Azure Static Web Apps の CLI を使ってローカル開発を試してみた](https://zenn.dev/microsoft/articles/static-web-apps-cli-getting-start#azure-static-web-apps)

###### 2-5-3-1-1 環境変数の設定

```bash
export LIFF_ID=<LIFFアプリID>
export BASE_HOSTNAME=<Azure Static Web Appsのホスト名>

echo "LIFF_ID=${LIFF_ID}" > frontend/.env
echo "BASE_URL=https://${BASE_HOSTNAME}" >> frontend/.env
```

###### 2-5-3-1-2 Azure Static Web Appsのデプロイ

1. [Azure Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli)をインストールして、初期化を行います。

```bash
npx @azure/static-web-apps-cli init
```

Global インストールしちゃったほうが楽かも。

<!-- ローカルで実行する場合は以下のコマンドを実行する。

```bash
npx @azure/static-web-apps-cli start ./frontend --api-location ./backend
```

Node.js v20.10.0 で実行したところ
> ✖ Found Azure Functions Core Tools v4 which is incompatible with your current Node.js v20.10.0.
> ✖ See https://aka.ms/functions-node-versions for more information.
となったため`Node.js v18.19.0`で実行します。 -->

2. フロントエンドのビルドを行います。

```bash
cd frontend

npm install
# https://v2.nuxt.com/deployments/azure-static-web-apps/
npm run generate

cd..
```

3. デプロイを行います。

```bash
deployment_token=<デプロイトークン>
# deployment_token=$(az staticwebapp secrets list --name <Azure Static Web Appsのアプリ名> --query "properties.apiKey" -o tsv)
npx @azure/static-web-apps-cli deploy --env production --deployment-token ${deployment_token}
``` 

##### 2-5-3-2 [Azureへデプロイしたバックエンドの設定と初期データの投入](https://github.com/line/line-api-use-case-smart-retail-azure/blob/main/docs/jp/backend-deployment.md)

##### 2-5-3-2-1 環境変数の設定

```bash
az staticwebapp appsettings set --name <Azure Static Web Appsのアプリ名> --setting-names \
  LineOptions__ChannelId=<Messaging APIチャネルのチャネルID> \
  LineOptions__LoginChannelId=<LINEログインチャネルのチャネルID> \
  LinePayOptions__ChannelId=<LINE PayのチャネルID> \
  LinePayOptions__ChannelSecret=<LINE Payのチャネルシークレット>
```

##### 2-5-3-2-2 Cosmos DBへのマスタデータ登録

1. ファイアウォール設定の変更

```bash
# Cosmos DBアカウント名とリソースグループ名を設定
# Cosmos DBアカウント名はAzure Cosmos DBインスタンスを識別し、アクセスするために使用される。
# Azure Cosmos DBのURLの一部としても使用される。
# https://${cosmosdb_account}.documents.azure.com:443/ 
cosmosdb_account="<Cosmos DBアカウント名>"
resource_group="<リソースグループ名>"

# ファイアウォール設定を更新
# 結構時間がかかる
az cosmosdb update --name $cosmosdb_account --resource-group $resource_group --ip-range-filter "<作業元のIPアドレス>"
```

2. データベースとコンテナの作成

```bash
# データベースの作成
db_name=LineApiUseCaseSmartRetail
az cosmosdb sql database create --account-name $cosmosdb_account --resource-group $resource_group --name $db_name

# コンテナの作成
# スラッシュで始まるテキストが勝手に、Windowsのパスに変換されて補われてしまう問題があるため、MSYS_NO_PATHCONV=1を設定する。
export MSYS_NO_PATHCONV=1
az cosmosdb sql container create --account-name $cosmosdb_account --resource-group $resource_group --database-name $db_name --name coupons --partition-key-path "/couponId"
az cosmosdb sql container create --account-name $cosmosdb_account --resource-group $resource_group --database-name $db_name --name items --partition-key-path "/barcode"
az cosmosdb sql container create --account-name $cosmosdb_account --resource-group $resource_group --database-name $db_name --name lineChannel --partition-key-path "/channelId"
```

| コンテナ名 | pk |
| --- | --- |
| coupons | /couponId |
| items | /barcode |
| lineChannel | /channelId |

3. データの追加
Azure CLIでは直接Cosmos DBにデータを追加する機能は提供されていないようなので、[Cosmos DBのデータエクスプローラー](https://docs.microsoft.com/ja-jp/azure/cosmos-db/data-explorer)を使用してデータを追加します。
データの追加はコンテナ配下の[items]を選択し、[New Item]から新規レコードを作成します。

couponsに追加するデータ

```json
{
  "barcode": "4956022006116",
  "couponDescription": "【感謝価格】すいか20%割引",
  "couponId": "watermelon_coupon",
  "deleted": "",
  "discountEndDatetime": "2022-12-31 23:59:000",
  "discountRate": 20,
  "discountStartDatetime": "2021-04-01 00:00:000",
  "discountWay": 2,
  "imageUrl": "https://media.istockphoto.com/vectors/watermelon-icon-in-trendy-flat-style-isolated-on-white-background-vector-id877064160?s=612x612",
  "itemName": "すいか",
  "remarks": "すいか１点につき、20円引きとなります。"
}
```

itemsに追加するデータ

```json
{
  "barcode": "4956022006116",
  "imageUrl": "https://media.istockphoto.com/vectors/watermelon-icon-in-trendy-flat-style-isolated-on-white-background-vector-id877064160?s=612x612",
  "itemName": "すいか",
  "itemPrice": 100
}
```

```json
{
  "barcode": "1230059783947",
  "imageUrl": "https://media.gettyimages.com/vectors/stack-of-books-vector-id504374218?s=2048x2048",
  "itemName": "書籍",
  "itemPrice": 100
}
```

```json
{
  "barcode": "2130627341496",
  "imageUrl": "https://media.gettyimages.com/vectors/tomato-flat-design-vegetable-icon-vector-id1017915086?s=2048x2048",
  "itemName": "とまと",
  "itemPrice": 50
}
```

```json
{
  "barcode": "8358328475935",
  "imageUrl": "https://media.gettyimages.com/vectors/stack-of-books-vector-id504374218?s=2048x2048",
  "itemName": "書籍",
  "itemPrice": 100
}
```

```json
{
  "barcode": "84895769",
  "imageUrl": "https://media.istockphoto.com/vectors/simple-apple-in-flat-style-vector-illustration-vector-id1141529240?s=612x612",
  "itemName": "りんご",
  "itemPrice": 50
}
```

lineChannelに追加するデータのテンプレート

```json
{
    "channelId": "Messaging APIチャネルのチャネルID",
    "channelSecret": "Messaging APIチャネルのチャネルシークレット",
    "channelAccessToken": "Messaging APIチャネルのチャネルトークン",
    "limitDate": "2021-01-01T00:00:00.0000000+00:00",
    "updatedTime": "2021-01-01T00:00:00.0000000+00:00"
}
```

#### 2-5-4 動作確認

以下の設置を行った後に、動作確認を行います。
すべての手順が完了後、LIFF URLにアクセスし、動作を確認してください。

##### 2-5-4-1 [LIFFエンドポイントの設定](https://github.com/line/line-api-use-case-smart-retail-azure/blob/main/docs/jp/validation.md#liff%E3%82%A8%E3%83%B3%E3%83%89%E3%83%9D%E3%82%A4%E3%83%B3%E3%83%88%E3%81%AE%E8%A8%AD%E5%AE%9A)

【LINEチャネルの作成 -> LIFFアプリの追加】にて作成したLIFFアプリのエンドポイントURLを設定します。

1. [LINE Developersコンソール](https://developers.line.biz/console/)にて、LINEログインチャンネルの画面の[LIFE]タブをクリックしてLIFEアプリ一覧を表示します。
2. 作成したLIFEアプリをクリックします。
3. [エンドポイントURL]に`https://<Azure Static Web Appsのホスト名>`を設定します。

##### 2-5-4-2 [リッチメニューの設定](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)

ToDo



### 2-5 ローカル実行手順

#### 2-5-1 [バックエンド ローカル実行手順](https://github.com/line/line-api-use-case-smart-retail-azure/blob/main/docs/jp/backend-deployment.md#%E3%83%90%E3%83%83%E3%82%AF%E3%82%A8%E3%83%B3%E3%83%89-%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E5%AE%9F%E8%A1%8C%E6%89%8B%E9%A0%86)

##### 2-5-1-1 環境

###### 2-5-1-1-1 [Azure Functions for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
###### 2-5-5-1-2 [Cosmos DB Emulator](https://docs.microsoft.com/ja-jp/azure/cosmos-db/local-emulator)

- [Cosmos DB Emulator Recipes](https://github.com/Azure/cosmosdb-emulator-recipes/tree/main)
- [Docker for Windows 環境で Linuxコンテナ版 Azure Cosmos DB emulator 起動](https://qiita.com/kazumihirose/items/24fc49843c763f799b46)

1. イメージのPullと実行

```bash
docker pull mcr.microsoft.com/cosmosdb/linux/azure-cosmos-emulator:latest
docker run -p 8081:8081 -p 10251:10251 -p 10252:10252 -p 10253:10253 -p 10254:10254 -m 3g --cpus=2.0 --name=test-linux-emulator -e AZURE_COSMOS_EMULATOR_PARTITION_COUNT=10 -e AZURE_COSMOS_EMULATOR_ENABLE_DATA_PERSISTENCE=true -it mcr.microsoft.com/cosmosdb/linux/azure-cosmos-emulator:latest
```

2. エミュレーター用の証明書の取得

[https://localhost:8081/_explorer/emulator.pem](https://localhost:8081/_explorer/emulator.pem)をダウンロードし、インストールします。
PowerShellを管理者権限で起動し、以下のコマンドを実行します。

```powershell
$cert_url = "https://localhost:8081/_explorer/emulator.pem"
$cert_path = "$env:USERPROFILE\Downloads\emulator.pem"

# SSL/TLSの検証を無視する設定
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = { $true }

# 証明書のダウンロード
# Invoke-WebRequest が予期せぬエラーで使えなかったので代わりに System.Net.WebClient クラスを使用
$webClient = New-Object System.Net.WebClient
$webClient.DownloadFile($cert_url, $cert_path)

# 証明書のインストール
Import-Certificate -FilePath $cert_path -CertStoreLocation Cert:\LocalMachine\Root
# certutil -addstore -f "Root" $cert_path # でもたぶんOK
```

ローカル管理画面にアクセス
[https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)

##### 2-5-1-2 ファイル、データの準備

1. `local.settings.json`の準備

- LINE Payの決済をテストする場合に必要な項目
    - LINEチャネルID
    - LINEログインのチャネルID
    - LINE PayのチャネルID、シークレット
    - (フロントエンドから接続して動作確認する場合)各種URL
    - http://localhost/~ のものが該当
    - CosmosDbAccount Cosmos DBのアカウントURL(ローカルでCosmosDBエミュレータを使う場合はテンプレートファイルのままでOK)
    - CosmosDbKey Cosmos DBのキー(ローカルでCosmosDBエミュレータを使う場合はテンプレートファイルのままでOK)

```json:local.settings.json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "ApplicationOptions__DetailsUrl": "http://localhost/history.html",
    "LineOptions__ChannelId": "<LINE_CHANNEL_ID>",
    "LineOptions__LoginChannelId": "<LINE_LOGIN_CHANNEL_ID>",
    "LinePayOptions__ChannelId": "<LINEPAY_CHANNEL_ID>",
    "LinePayOptions__ChannelSecret": "<LINEPAY_CHANNEL_SECRET>",
    "LinePayOptions__PaymentImageUrl": "http://localhost/dummy",
    "LinePayOptions__ConfirmUrl": "http://localhost/completed.html",
    "LinePayOptions__CancelUrl": "http://localhost/smaphregi/",
    "CosmosDbAccount": "https://localhost:8081/",
    "CosmosDbKey": "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="
  }
}
```

コマンドで生成する場合は以下の通り。

```bash
# local.settings.json ファイル生成
touch backend/src/LineApiUseCaseSmartRetail/local.settings.json

# local.settings.json ファイルに値を設定
# LINEチャネルID
# LINEログインのチャネルID
# LINE PayのチャネルID、シークレット
# (フロントエンドから接続して動作確認する場合)各種URL
# http://localhost/~ のものが該当
# CosmosDbAccount Cosmos DBのアカウントURL(ローカルでCosmosDBエミュレータを使う場合はテンプレートファイルのままでOK)
# CosmosDbKey Cosmos DBのキー(ローカルでCosmosDBエミュレータを使う場合はテンプレートファイルのままでOK)
cat << EOS > backend/src/LineApiUseCaseSmartRetail/local.settings.json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "ApplicationOptions__DetailsUrl": "http://localhost/history.html",
    "LineOptions__ChannelId": "<LINE_CHANNEL_ID>",
    "LineOptions__LoginChannelId": "<LINE_LOGIN_CHANNEL_ID>",
    "LinePayOptions__ChannelId": "<LINEPAY_CHANNEL_ID>",
    "LinePayOptions__ChannelSecret": "<LINEPAY_CHANNEL_SECRET>",
    "LinePayOptions__PaymentImageUrl": "http://localhost/dummy",
    "LinePayOptions__ConfirmUrl": "http://localhost/completed.html",
    "LinePayOptions__CancelUrl": "http://localhost/smaphregi/",
    "CosmosDbAccount": "https://localhost:8081/",
    "CosmosDbKey": "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="
  }
}
EOS
```

2. Cosmos DBへのマスタデータ登録

[2-5-3-2-2 Cosmos DBへのマスタデータ登録](#2-5-3-2-2-cosmos-dbへのマスタデータ登録)の[2. データベースとコンテナの作成]と[3. データの追加]をローカルで実施します。
[エミュレーターに対してはAzure CLIは使用できない](https://github.com/Azure/azure-cli/issues/17957#issuecomment-836084708)そうなので、[REST API](https://learn.microsoft.com/en-us/rest/api/cosmos-db/)を直接叩く必要があります。

REAT API用の認証トークンを生成するNode.jsスクリプトを作成

```bash
# Node.jsスクリプトを作成
touch create_cosmos_db_auth_token.js

# Node.jsスクリプトに値を設定
# Node.js 18.19.0 で実行を想定
cat << EOS > create_cosmos_db_auth_token.js
var crypto = require("crypto");  

// Azure Cosmos DBのREST APIを使用する際には、Authorizationヘッダーが必要です。
// このヘッダーは、特定のリクエストに対する署名を提供します。
// 以下に、Authorizationヘッダーを生成するために必要な各パラメータの詳細を示します。
// - verb: これはHTTPメソッド（GET、POST、PUT、DELETEなど）を表します。例えば、データを追加する場合は"POST"を使用します。
// - resourceType: これは操作対象のリソースの種類を表します。例えば、コンテナを作成する場合は"dbs", データを追加する場合は"docs"を使用します。
// - resourceLink: これは操作対象のリソースへのリンクを表します。例えば、データベース名がmyDatabaseで、コンテナ名がmyContainerの場合、リソースリンクは"dbs/myDatabase/colls/myContainer"となります。
// - date: これはリクエストの日付を表します。これはUTCの日付で、RFC 1123形式である必要があります。シェルスクリプトでは$(date -u)を使用して生成できます。
function getAuthorizationTokenUsingMasterKey(verb, resourceType, resourceId, date, masterKey) {
    var key = Buffer.from(masterKey, "base64");

    var text = (verb || "").toLowerCase() + "\n" +
               (resourceType || "").toLowerCase() + "\n" +
               (resourceId || "") + "\n" +
               date.toLowerCase() + "\n" +
               "" + "\n";

    var body = Buffer.from(text, "utf8");
    var signature = crypto.createHmac("sha256", key).update(body).digest("base64");

    var MasterToken = "master";
    var TokenVersion = "1.0";

    return encodeURIComponent("type=" + MasterToken + "&ver=" + TokenVersion + "&sig=" + signature);
}

// コマンドライン引数を受け取る
var args = process.argv.slice(2);
var verb = args[0];
var resourceType = args[1];
var resourceId = args[2];
var date = args[3];
var masterKey = args[4];

var token = getAuthorizationTokenUsingMasterKey(verb, resourceType, resourceId, date, masterKey);

console.log(token);
EOS
```

データベースを作成

```bash
endpoint="https://localhost:8081/"
masterKey="C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="
dbName="LineApiUseCaseSmartRetail"

verb="post"
resourceType="dbs"
resourceLink=""
date=$(date -u "+%a, %d %b %Y %H:%M:%S GMT")

# Node.jsスクリプトを実行してトークンを生成
authHeader=$(node.exe create_cosmos_db_auth_token.js "$verb" "$resourceType" "$resourceLink" "$date" "$masterKey")

echo $authHeader

# データベースを作成するためのJSON本体
requestBody="{\"id\":\"$dbName\"}"

# データベースを作成
curl -k -X POST -H "Content-Type: application/json" \
     -H "x-ms-version: 2018-12-31" \
     -H "x-ms-date: $date" \
     -H "Authorization: $authHeader" \
     --data "$requestBody" \
     $endpoint"dbs"
```

コンテナの作成

```bash
date=$(date -u "+%a, %d %b %Y %H:%M:%S GMT")

# コンテナを作成する関数
create_container() {
    local containerName=$1
    local partitionKey=$2

    # コンテナを作成するためのJSON本体（インデックスポリシーを省略）
    local requestBody='{  
        "id": "'$containerName'",  
        "indexingPolicy": {  
            "automatic": true,  
            "indexingMode": "Consistent",  
            "includedPaths": [  
            {  
                "path": "/*"
            }  
            ],
            "excludedPaths": [
            {
                "path": "/\"_etag\"/?"
            }
        ]
        },  
        "partitionKey": {  
            "paths": [  
            "'$partitionKey'"  
            ],  
            "kind": "Hash",
            "Version": 2
        }  
    }'
    
    # トークンを生成
    local authHeader=$(node.exe create_cosmos_db_auth_token.js "post" "colls" "dbs/$dbName" "$date" "$masterKey")

    # コンテナを作成
    curl -k -X POST -H "Content-Type: application/json" \
         -H "x-ms-version: 2018-12-31" \
         -H "x-ms-date: $date" \
         -H "Authorization: $authHeader" \
         --data "$requestBody" \
         $endpoint"dbs/$dbName/colls"
}

# 各コンテナを作成
create_container "coupons" "/couponId"
create_container "items" "/barcode"
create_container "lineChannel" "/channelId"
```

データの追加

```bash
date=$(date -u "+%a, %d %b %Y %H:%M:%S GMT")

# データを追加する関数
add_data_to_container() {
    local containerName=$1
    local data=$2
    local partitionKeyValue=$3  # パーティションキーの値を追加

    # UUIDを生成
    local docId=$(powershell -Command "[guid]::NewGuid().ToString()")
    

    # データにUUIDを追加
    local modifiedData=$(echo $data | jq --arg docId "$docId" '. + {id: $docId}')

    # トークンを生成
    local authHeader=$(node.exe create_cosmos_db_auth_token.js "post" "docs" "dbs/$dbName/colls/$containerName" "$date" "$masterKey")

    # データを追加
    curl -k -X POST -H "Content-Type: application/json" \
         -H "x-ms-version: 2018-12-31" \
         -H "x-ms-date: $date" \
         -H "Authorization: $authHeader" \
         -H "x-ms-documentdb-partitionkey: [\"$partitionKeyValue\"]" \
         --data "$modifiedData" \
         $endpoint"dbs/$dbName/colls/$containerName/docs"
}


# couponsコンテナにデータを追加
add_data_to_container "coupons" '{
  "barcode": "4956022006116",
  "couponDescription": "【感謝価格】すいか20%割引",
  "couponId": "watermelon_coupon",
  "deleted": "",
  "discountEndDatetime": "2022-12-31 23:59:000",
  "discountRate": 20,
  "discountStartDatetime": "2021-04-01 00:00:000",
  "discountWay": 2,
  "imageUrl": "https://media.istockphoto.com/vectors/watermelon-icon-in-trendy-flat-style-isolated-on-white-background-vector-id877064160?s=612x612",
  "itemName": "すいか",
  "remarks": "すいか１点につき、20円引きとなります。"
}' "watermelon_coupon"


# itemsコンテナにデータを追加
add_data_to_container "items" '{
  "barcode": "4956022006116",
  "imageUrl": "https://media.istockphoto.com/vectors/watermelon-icon-in-trendy-flat-style-isolated-on-white-background-vector-id877064160?s=612x612",
  "itemName": "すいか",
  "itemPrice": 100
}'

add_data_to_container "items" '{
  "barcode": "1230059783947",
  "imageUrl": "https://media.gettyimages.com/vectors/stack-of-books-vector-id504374218?s=2048x2048",
  "itemName": "書籍",
  "itemPrice": 100
}'

add_data_to_container "items" '{
  "barcode": "2130627341496",
  "imageUrl": "https://media.gettyimages.com/vectors/tomato-flat-design-vegetable-icon-vector-id1017915086?s=2048x2048",
  "itemName": "とまと",
  "itemPrice": 50
}'

add_data_to_container "items" '{
  "barcode": "8358328475935",
  "imageUrl": "https://media.gettyimages.com/vectors/stack-of-books-vector-id504374218?s=2048x2048",
  "itemName": "書籍",
  "itemPrice": 100
}'

add_data_to_container "items" '{
  "barcode": "84895769",
  "imageUrl": "https://media.istockphoto.com/vectors/simple-apple-in-flat-style-vector-illustration-vector-id1141529240?s=612x612",
  "itemName": "りんご",
  "itemPrice": 50
}'


# lineChannelコンテナにデータを追加
add_data_to_container "lineChannel" '{
    "channelId": "Messaging APIチャネルのチャネルID",
    "channelSecret": "Messaging APIチャネルのチャネルシークレット",
    "channelAccessToken": "Messaging APIチャネルのチャネルトークン",
    "limitDate": "2021-01-01T00:00:00.0000000+00:00",
    "updatedTime": "2021-01-01T00:00:00.0000000+00:00"
}'
```
