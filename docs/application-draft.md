# SIWC利用申請の準備下書き

作成・公式窓口確認日：2026年10月10日  
状態：本人レビュー用の下書き。フォームへの入力・送信、クライアント登録、承認取得は未実施。

## 申請の目的と現在の段階

「会話で音楽を学ぶ実験室」は、初心者がブラウザでリズムを聴き比べ、自分で編集し、AIとの対話で変化を理解する音楽学習Webアプリの企画である。本プロジェクトは収益化を行わない。実際のSIWCと、利用者が許可した本人のChatGPTプランによる推論を使い、利用者ごとの認証情報・ログイン状態・会話・リズムパターンを分離することを目標とする。

現在は非公開の企画段階で、実装、実認証・実推論試験は未開始である。開発場所はCodexクラウド。初回認証試験はmacOSの同一PC上のブラウザ＋ローカルバックエンドに計画上選定済みだが、実行準備も未実施である。本番アプリの実行場所と提供構成は別途決める。LANまたは遠隔の共有バックエンドに複数利用者が同時接続する構成は候補であり、適用条件と必要な承認は未確認である。

自作部分はMITライセンスで、将来OSS公開を予定する。第三者コード・素材は元の条件に従い、SIWC DevKitを採用する場合の独自ライセンスは別に確認する。DevKitは未導入であり、自作部分のMITや非収益化の方針をSIWCサービス利用許可と扱わない。

## 公式窓口と表示項目

[ChatGPTプラン利用の概要](https://developers.openai.com/siwc/token-sharing-open-source)は、遠隔ホスト型または有料のアプリについて[Interest form](https://openai.com/form/sign-in-with-chatgpt-interest/)を案内している。[client ID申請案内](https://developers.openai.com/siwc/request-client-id)とフォーム本文は選定された商用パートナー向けの案内であり、個人の非収益化案件の受付方法は未確認である。このフォームを正式な受付先と決める前に、その点を確認する。

以下は閲覧時の必須表示を整理したもの。送信時の検証規則や追加要求を保証しない。本人情報の実値は本書へ保存せず、正式な窓口と記入方法を確認後、本人が送信先へ直接記入する。

| 表示項目 | 必須表示 | 下書き・対応 |
|---|---|---|
| Work email | あり | ［本人記入：連絡先メール。個人案件での記入方法を確認］ |
| First name | あり | ［本人記入：名］ |
| Last name | あり | ［本人記入：姓］ |
| Company name | あり | ［本人記入：個人案件で認められる記入方法を確認］ |
| Website URL | あり | ［本人判断：受理されるURLの種類と公開範囲を確認］ |
| Job title | なし | ［本人判断：任意記入］ |
| 希望機能 | あり | サインイン＋ChatGPTプランによるAIリクエストを希望 |
| 対象製品の簡潔な説明 | あり | 下記の日英説明をレビューして使用 |

表示本文からは、完成アプリ、デモ、公開GitHubリポジトリが必須かは確認できない。不要とも判断しない。非公開リポジトリを公開URLの代わりに提出すると決めず、URLの要件と企画段階の受付可否を確認する。会社・業務用メールを架空の情報で補わない。[公式フォーム](https://openai.com/form/sign-in-with-chatgpt-interest/)

## 製品説明の日本語下書き

会話で音楽を学ぶ実験室は、初心者がブラウザでリズムを聴き比べ、グリッド上で音の位置を編集し、AIに「なぜ違って聴こえるか」を質問する、個人運営の非収益化Webアプリの企画です。音の再生はブラウザ側で行い、AIとの対話にはリズムの構造化データとテキストを使う初期案を検討しています。

実際のSign in with ChatGPTを通じて、利用者が許可した本人のChatGPTプランでAIリクエストを実行することを希望します。利用者ごとの認証情報、ログイン状態、会話、リズムパターンを分離する設計と実動作検証を目指します。現在は非公開の企画段階で、実装・実認証・実推論試験は未開始です。初回はmacOS上のローカル構成で試験する計画ですが、将来のLANまたは遠隔共有バックエンドの提供条件、必要な承認、登録方式、運営者による資格情報の保管・更新について確認したいと考えています。本番の実行場所は未決定です。

自作部分はMITライセンスで将来OSS公開を予定しています。SIWC DevKitの採用・ライセンス適合性とSIWCサービス利用許可は別に確認します。個人の非収益化案件の適切な申請窓口、企画段階での受付可否、必要なURL・資料をご案内ください。

## English product description draft

Conversational Music Lab is a planned, individually operated, non-monetized browser-based music learning app for beginners. Users would compare rhythm patterns, edit note positions on a grid, and ask an AI why the patterns sound different. The initial concept uses browser-side audio playback and structured rhythm data plus text for AI dialogue.

We would like to integrate actual Sign in with ChatGPT and, with each user's permission, use that user's own ChatGPT plan for AI requests. Our goals include separating credentials, login sessions, conversations, and rhythm patterns between users and verifying that separation in practice. The project is currently in private planning; implementation, real authentication, and inference tests have not started. The first authentication test is planned on a single macOS computer with a browser and local backend. A future LAN or remotely hosted backend serving multiple independent users remains a candidate, and the production hosting location is undecided. We seek guidance on eligibility, required approval, client registration, and whether the operator may store and refresh each user's credentials for that configuration.

The independently authored portions use the MIT license and are intended for future open-source release. Any adoption of the SIWC DevKit and its separate license will be assessed separately from permission to use the SIWC service. Please advise on the appropriate application route for an individual, non-monetized project, whether a planning-stage proposal can be considered, and the required URL or supporting materials.

## 承認側へ確認する質問

1. 個人の非収益化・将来OSS公開の企画はこの窓口の対象か。対象外なら適切な公式窓口はどこか。会社名・業務用メール欄をどう記入すべきか。
2. 企画段階で相談・申請できるか。Website URLに求める内容は何か。公開リポジトリ、デモ、完成アプリはどの段階で必要か。
3. LAN共有と遠隔共有のそれぞれで、独立した複数利用者が本人のChatGPTプランを使う構成は対象か。必要な承認、登録方式、callback、user/workspace/client/hostの対応を確認したい。
4. 共有構成で運営者が利用者ごとの資格情報を保管・更新できるか。必要な同意、アクセス分離、削除・失効条件は何か。
5. 利用資格のあるプラン、ワークスペース、地域の範囲は何か。
6. DevKitを採用する場合、本用途への独自ライセンスの適合性と、自作MIT部分との配布上の境界について別途確認したい。

質問3・4は共有構成の条件確認であり、ローカル試験や同一利用者の自己所有VMの説明から共有サービスの許可を推定しない。技術的な背景は[調査記録](siwc-research.md)、試験の範囲は[認証試験計画](auth-test-plan.md)を参照する。

## 本人の判断・記入欄

- ［本人判断：日英説明の内容と、申請する提供形態の範囲］
- ［本人判断：相談窓口と個人案件の受付方法の確認結果］
- ［本人判断：Website URL・添付資料の要件、公開してよい資料と公開時期］
- ［本人記入：申請者情報は正式な送信先へ直接記入。本書へ実値を追記しない］
- ［本人判断：送信時期と送信する最終文面］

申請準備下書きの承認、フォーム送信、OpenAIによる利用承認、リポジトリ公開、実装開始はそれぞれ別の状態として記録する。今回完了するのは下書き作成のみであり、フォーム入力・送信、公開、実装、設定変更は行わない。
