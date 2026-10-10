# SIWC Interest formの送信・受付記録と準備時の説明案

作成・公式窓口確認日：2026年10月10日  
状態：2026年10月10日 18:33 JST、リポジトリ設定画面でpublicを確認し、公式SIWC Interest formを送信した。画面の「お問い合わせを受け付けました」「製品が対象となる場合は、ご連絡いたします」で受付を確認した。これは利用承認ではない。アプリ実装、クライアント登録、実認証・実推論試験、ホスト型での利用承認取得は未実施。

公開URL：[conversational-music-lab](https://github.com/tom7808/conversational-music-lab)

個人の非収益化企画の受付可否と、ホスト型Webアプリで各利用者本人のChatGPTプランを使う条件を問い合わせた。以下の日英説明案・質問と実送信文面の完全一致は未確認であり、実送信文面の転載ではない。申請者の氏名・メール、Company name・Job titleの入力値、認証情報は本書に保存しない。メール返信の有無は本記録では確認していない。

## 申請の目的と現在の段階

「会話で音楽を学ぶ実験室」は、初心者がブラウザでリズムを聴き比べ、自分で編集し、AIとの対話で変化を理解する音楽学習Webアプリの企画である。本プロジェクトは収益化を行わない。実際のSIWCと、利用者が許可した本人のChatGPTプランによる推論を使い、利用者ごとの認証情報・ログイン状態・会話・リズムパターンを分離することを目標とする。

現在は企画文書の公開段階で、実装、実認証・実推論試験は未開始である。開発場所はCodexクラウド。初回認証試験はmacOSの同一PC上のブラウザ＋ローカルバックエンドに計画上選定済みだが、実行準備も未実施である。申請対象は、複数の利用者がそれぞれのChatGPTアカウントで使うホスト型Webアプリに決定済みである。ローカル環境は本番提供形態ではなく、事前検証用に限る。本番の具体的なホスト先は未決定であり、ホスト型での適用条件と必要な承認は未確認である。

企画文書を公開する段階であり、将来実装する自作コードはMITライセンスでOSS公開を予定する。第三者コード・素材は元の条件に従い、SIWC DevKitを採用する場合の独自ライセンスは別に確認する。DevKitは未導入であり、自作部分のMITや非収益化の方針をSIWCサービス利用許可と扱わない。

## 公式窓口と表示項目

[ChatGPTプラン利用の概要](https://developers.openai.com/siwc/token-sharing-open-source)は、遠隔ホスト型または有料のアプリについて[Interest form](https://openai.com/form/sign-in-with-chatgpt-interest/)を案内している。[client ID申請案内](https://developers.openai.com/siwc/request-client-id)とフォーム本文は選定された商用パートナー向けの案内であり、個人の非収益化案件の受付方法は未確認である。このInterest formへの送信と画面上の受付確認は完了したが、個人の非収益化企画が対象となるかは未確認である。

以下は準備時に閲覧した表示項目の記録であり、送信内容や入力値の記録ではない。送信時の検証規則や追加要求を保証しない。本人情報の実値を本書へ保存しない方針は維持する。

| 表示項目 | 必須表示 |
|---|---|
| Work email | あり |
| First name | あり |
| Last name | あり |
| Company name | あり |
| Website URL | あり |
| Job title | なし |
| 希望機能 | あり |
| 対象製品の簡潔な説明 | あり |

表示本文からは、完成アプリ、デモ、公開GitHubリポジトリが必須かは確認できない。不要とも判断しない。必要資料の条件は未確認である。[公式フォーム](https://openai.com/form/sign-in-with-chatgpt-interest/)

## 準備時の日本語説明案（実送信文面の転載ではない）

会話で音楽を学ぶ実験室は、初心者がブラウザでリズムを聴き比べ、グリッド上で音の位置を編集し、AIに「なぜ違って聴こえるか」を質問する、個人運営の非収益化ホスト型Webアプリの企画です。音の再生はブラウザ側で行い、AIとの対話にはリズムの構造化データとテキストを使う初期案を検討しています。

実際のSign in with ChatGPTを通じて、利用者が許可した本人のChatGPTプランでAIリクエストを実行することを希望します。利用者ごとの認証情報、ログイン状態、会話、リズムパターンを分離する設計と実動作検証を目指します。現在は企画文書の公開段階で、実装・実認証・実推論試験は未開始です。申請対象は、複数の利用者がそれぞれのChatGPTアカウントで使うホスト型Webアプリです。macOS上のローカル構成は事前検証用に限り、本番の具体的なホスト先は未決定です。このホスト型提供の適用条件、必要な承認、登録方式、運営者による利用者ごとの資格情報の保管・更新について確認したいと考えています。ホスト型での利用承認はまだ取得していません。

企画文書を公開する段階であり、将来実装する自作コードはMITライセンスでOSS公開を予定しています。SIWC DevKitの採用・ライセンス適合性とSIWCサービス利用許可は別に確認します。個人の非収益化案件の適切な申請窓口、企画段階での受付可否、必要なURL・資料をご案内ください。

## English preparation draft (not a copy of the submitted text)

Conversational Music Lab is a planned, individually operated, non-monetized hosted web app that helps beginners learn music. Users would compare rhythm patterns, edit note positions on a grid, and ask an AI why the patterns sound different. The initial concept uses browser-side audio playback and structured rhythm data plus text for AI dialogue.

We would like to integrate actual Sign in with ChatGPT and, with each user's permission, use that user's own ChatGPT plan for AI requests. Our goals include separating credentials, login sessions, conversations, and rhythm patterns between users and verifying that separation in practice. The project is at the stage of publishing planning documents; implementation, real authentication, and inference tests have not started. The application scope is a hosted web app used by multiple independent users, each with their own ChatGPT account. A browser and local backend on a single macOS computer are planned solely for preliminary testing. The specific production hosting location is undecided. Eligibility and approval for this hosted offering have not been confirmed. We seek guidance on the applicable conditions, required approval, client registration, and whether the operator may store and refresh each user's credentials for this configuration.

We are at the stage of publishing planning documents, and intend to release future independently authored code as open source under the MIT license. Any adoption of the SIWC DevKit and its separate license will be assessed separately from permission to use the SIWC service. Please advise on the appropriate application route for an individual, non-monetized project, whether a planning-stage proposal can be considered, and the required URL or supporting materials.

## 準備時の確認質問案（実送信内容の列挙ではない）

1. 個人の非収益化・企画文書の公開段階にあり将来コードもOSS公開する企画はこの窓口の対象か。対象外なら適切な公式窓口はどこか。会社名・業務用メール欄をどう記入すべきか。
2. 企画段階で相談・申請できるか。Website URLに求める内容は何か。公開リポジトリ、デモ、完成アプリはどの段階で必要か。
3. 申請対象のホスト型Webアプリで、独立した複数利用者がそれぞれ本人のChatGPTアカウントとプランを使う構成は対象か。必要な承認、登録方式、callback、user/workspace/client/hostの対応を確認したい。
4. 共有構成で運営者が利用者ごとの資格情報を保管・更新できるか。必要な同意、アクセス分離、削除・失効条件は何か。
5. 利用資格のあるプラン、ワークスペース、地域の範囲は何か。
6. DevKitを採用する場合、本用途への独自ライセンスの適合性と、自作MIT部分との配布上の境界について別途確認したい。

質問3・4は共有構成の条件確認であり、ローカル試験や同一利用者の自己所有VMの説明から共有サービスの許可を推定しない。技術的な背景は[調査記録](siwc-research.md)、試験の範囲は[認証試験計画](auth-test-plan.md)を参照する。

## 送信後に残る確認

フォーム送信と画面上の受付確認は完了したため、本人情報の入力や送信時期を送信前のTodoとして扱わない。個人の非収益化企画の対象可否、ホスト型で各利用者のChatGPTプランを使う条件、必要資料・登録・承認は引き続き未確認である。

リポジトリのpublic確認、フォーム送信・受付確認、OpenAIによる利用承認、実装開始はそれぞれ別の状態として記録する。企画文書は公開段階にあり、アプリ実装、クライアント登録、実認証・実推論試験、ホスト型での利用承認取得は未実施である。
