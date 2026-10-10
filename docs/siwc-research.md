# SIWC利用条件の調査記録

確認日：2026年10月10日

## 調査の到達点

公式資料の調査と未解決事項の記録を完了した。利用承認の取得、クライアント登録、実認証・実推論の検証は未実施である。フォームは閲覧のみで、入力・送信していない。

対象は、非収益化・自作部分MIT・将来OSS公開予定の音楽学習Webアプリである。利用者本人のChatGPTプランで推論し、複数利用者の認証・会話・パターンを分離する目標を維持する。共有バックエンドでの利用可否は未解決であり、非収益化やMIT採用だけで承認済みとは扱わない。

## 公式資料に明記された事項

### 対象プラン・利用資格

対象として明記されているのは利用資格のあるChatGPT Plus / Pro利用者である。サインインによる本人確認と、ChatGPTプランを使う権限は別で、利用者の許可が必要となる。ChatGPTの既存会話を取得する権限ではない。Free / Go / Business / Enterprise / Eduの利用可否を本調査から推定しない。[Quickstart](https://developers.openai.com/siwc/quickstart)

導入記事は、ローカルで動く個人プロジェクトとOSSツールの経路を説明し、有料または遠隔ホスト型は提供前のアクセス申請を案内している。ログイン成功やモデル一覧取得だけでなく、推論の完了まで確認する必要がある。[Cookbook](https://developers.openai.com/cookbook/articles/sign-in-with-chatgpt)

### 共有ホストとアカウントの違い

概要では、発行されたclient IDは利用者と登録時のワークスペースに結び付く。同じ利用者・ワークスペースの複数ホストで同一client IDを使えるが、ホストIDは各ホスト固有とされる。遠隔ホスト型のアプリには問い合わせフォームが案内されている。[プラン利用の概要](https://developers.openai.com/siwc/token-sharing-open-source)

アカウント管理資料は、保存した登録の選択・追加・切り替えを説明している。メールが同じでも登録と資格情報は分離し、他登録のclient IDとトークンを混ぜない。これは共有Webサービスの複数利用者同時接続に対する承認を明記したものではない。[Accounts and sessions](https://developers.openai.com/siwc/token-sharing-open-source/profiles-and-sessions)

自己所有VMの手順は明記されている。同じ利用者・ワークスペースのOAuthをローカルで完了し、選択した登録の保護済み資格情報を安全な経路でVMへ移す。VM固有のホストIDを維持し、その後の更新はVM側が担う。移したセッションについてホスト別の利用量帰属・プラン利用の失効は未対応とされる。[Self-hosted VMs](https://developers.openai.com/siwc/token-sharing-open-source/self-hosted-vms)

### 登録方式と認証後の戻り先

| 経路 | 明記された仕様 | 本プロジェクトへの意味 |
|---|---|---|
| OSS向け動的登録 | 初回は `dynamic_agent_client`、実際のアプリ名、永続的な `ext_agent_host_id` を送る。返却されたclient IDを登録単位で保持し、次回以降に使う。client secretやpartner API keyは不要。 | 事前発行のWebクライアントと混同しない。 |
| OSS向けcallback | 初回からHTTPの `127.0.0.1` を使う。後の認証で変更できるのはポートのみ。scheme・host・pathを保ち、同じ認証試行の認可要求とコード交換では完全に同じURIを使う。`localhost` に置き換えない。 | LANアドレスや公開HTTPS callbackへの置換を、現行の動的登録仕様からは導けない。 |
| Webサイト向け登録 | 事前発行client IDと環境ごとの正確な登録callback URLが必要。public / confidential clientに対応し、後者は登録された認証方式とsecretを使う。資料は本人確認の経路を扱う。 | Webログインができても、本人のプランによる推論権限を取得したことにはならない。 |

根拠：[Registration and sign-in](https://developers.openai.com/siwc/token-sharing-open-source/sign-in)、[On your website](https://developers.openai.com/siwc/website)

各認証試行でstate・nonce・PKCEを新しく作り、ID tokenの署名・issuer・audience・期限・nonceを検証する。推論前には付与された `chatgpt.tokens.use.direct` を確認する。ID token単独ではプラン利用を許可しない。[Registration and sign-in](https://developers.openai.com/siwc/token-sharing-open-source/sign-in)

### トークン保管とセッション

登録ごとの資格情報を保護されたローカルまたはself-hosted runtimeに保存する。ブラウザストレージ、Git、ログ、分析基盤にトークンを置かない。同一セッションのrefreshは直列化し、更新後のトークンを使用する。ログアウトでは遠隔失効の確認とローカル削除を区別する。[Accounts and sessions](https://developers.openai.com/siwc/token-sharing-open-source/profiles-and-sessions)

ファイル保存例は所有者のみの権限（Unixでは0600）と原子的な更新を要求する。[Registration and sign-in](https://developers.openai.com/siwc/token-sharing-open-source/sign-in)

仕様上、access tokenは1時間、refresh tokenは30日。正常なrefreshで新しい30日有効のrefresh tokenに置き換わる。これは仕様の確認であり、本アプリでの更新・失効動作は未検証である。[Token reference](https://developers.openai.com/siwc/token-sharing-open-source/token-reference)

### 推論の仕様と音楽アプリへの関係

選択中のアカウントのトークンでモデル一覧を取得し、同じアカウントで公開Responses APIを呼ぶ。HTTPでは `store:false` と `stream:true` を使い、`response.completed` を受信して初めて完了と判定する。[Models and inference](https://developers.openai.com/siwc/token-sharing-open-source/models-and-inference)

プレビューではHTTPで `previous_response_id` による継続を使わず、必要な履歴を入力へ含める。音声・動画入力と文字起こしAPIはこの経路では未対応とされる。[Preview limitations](https://developers.openai.com/siwc/token-sharing-open-source/preview-limitations)

本企画への解釈：ブラウザで音を再生し、リズムの構造化データについて対話する案と、音声そのものをモデルへ送る案は別である。前者の成立可能性を検討するが、実装適合性や学習効果の検証はまだ行っていない。

### DevKitのNoncommercial条件と自作部分のMIT

公式DevKitは利用者自身のマシンで動くOSSアプリ向けで、ローカルNode.js SDKとReact UI等を提供する。[DevKit README](https://github.com/openai/sign-in-with-chatgpt-devkit/blob/main/README.md)

DevKitのOpenAI作成コード・文書には独自のNoncommercial License v1.0が適用される。個人の学習・実験等でも、商用応用を意図または合理的に予見する用途は非商用の定義から外れる。事業者・雇用主・顧客の業務や商業上の利益に関する開発・試験・運用等は、料金を取らなくても対象外である。非営利団体であることだけでも十分ではない。

独立して書いたソフトウェアは、インターフェース経由の呼出し・リンク・通信だけでは改変物にならない。一方、DevKit自体の改変を配布する場合は同じライセンスを適用し、ライセンス・変更表示・所定の通知を保持する必要がある。OpenAI作成部分の商用利用は別の書面合意が必要で、同ライセンスはOpenAIサービスへのアクセス権を与えない。[DevKit LICENSE 第1・2・4・5節](https://github.com/openai/sign-in-with-chatgpt-devkit/blob/main/LICENSE)

本企画への解釈：独立した自作部分のMITと、DevKitを採用する場合の条件は分離する。MITを受けた他者が自作部分を商用利用できても、DevKitを含む全体を自由に商用利用できるという意味にはならない。現時点でDevKitは導入しておらず、条件への同意・適合性の確定も行っていない。

### 申請窓口・必要情報・プラグイン

申請フォームの必須表示は、業務用メール、名、姓、会社名、Website URL、希望機能、対象製品の説明。職名には必須表示がない。希望機能はサインインのみ／サインインとプラン利用の選択肢がある。フォーム自体は商用パートナー向けの案内であり、個人の非収益化・共有ホスト型OSSをどう記入するかは不明である。完成アプリ、公開GitHub URL、デモが必須とは表示本文から確認できないが、不要とも断定しない。[Interest form](https://openai.com/form/sign-in-with-chatgpt-interest/)

通常のclient ID申請案内も選定された商用パートナー向けのwaitlistを示す。[Request a client ID](https://developers.openai.com/siwc/request-client-id)

ChatGPTプラグイン内のSIWCは選定された商用パートナー向けの限定試験である。コネクター認可とOpenAI本人確認は別々のOAuth処理で、プラグイン公開や本人確認だけで本プロジェクトのプラン利用が承認されるわけではない。[In your ChatGPT plugin](https://developers.openai.com/siwc/chatgpt-plugin)

## 認証試験環境の判断材料（調査時点の比較）

追記：2026年10月10日に、初回試験は「macOS のローカル環境で、同一 PC 上のブラウザ＋ローカルバックエンド」へ計画上選定済みとなった。開発はCodexクラウドを維持する。以下は選定前の比較記録であり、最新の決定と未実施の試験は[試験計画](auth-test-plan.md)を参照する。共有構成の条件・承認は未解決のままである。

| 候補 | 判断材料 | 未解決事項 |
|---|---|---|
| 利用者のPC上のブラウザ＋ローカルruntime | loopback callbackと保護されたローカル保存に合わせやすいという推論。 | 配布方法・OS・保存方式を選ぶ必要。アカウント切り替え試験だけでは同時利用者分離の検証にならない。 |
| 同じ利用者のself-hosted VM | 公式のVM手順がある。ブラウザ側の127.0.0.1はVMを指さない。 | 資格情報移送とrefreshの責任、ホスト別失効の制約。本番の共有サービスへの一般化はしない。 |
| LAN共有／遠隔共有バックエンド | 今回確認した資料に、独立した複数利用者の同時利用を包括的に許可する明記は見つからない。 | 適用条件、承認経路、登録方式、callback、ホストID、資格情報の預かり方をOpenAIへ確認する。 |
| Codexクラウド | 作業・開発環境として決定済み。 | 本アプリの認証試験・実行環境としての適合は未決定。開発環境の決定を認証方式の承認と扱わない。 |

## OpenAIへ確認する事項

1. 無料・個人運営・自作MIT・将来OSS公開の音楽学習アプリで、LAN共有と遠隔共有それぞれに複数利用者を同時接続させ、本人のプランを使う構成は対象になるか。個人用VMの経路と何が異なるか。
2. この構成は動的登録か事前発行clientか。公開HTTPS callback、ブラウザ別のアプリセッション、user/workspace/client/hostの対応はどう定義するか。
3. 各利用者のトークンを運営者のサーバーで保管・更新することが認められるか。必要な分離・削除・失効条件は何か。
4. 非収益化の個人案件はどの窓口で申請し、会社名・業務用メールをどう記載するか。企画段階で申請できるか。公開リポジトリ・デモ・完成アプリの要否は何か。
5. Plus / Pro以外の資格、ワークスペースや地域による制約は何か。
6. DevKit利用・配布を選ぶ場合、本用途がNoncommercialの定義に適合するか。独立MIT部分との配布上の境界をどう示すか。

次は提供形態の候補と質問をレビューし、申請内容を準備する。今回の完了は調査記録の作成であり、条件確認の全解決や承認取得ではない。実装、公開化、申請送信、Projects操作、非公開の別保管領域更新は行っていない。

