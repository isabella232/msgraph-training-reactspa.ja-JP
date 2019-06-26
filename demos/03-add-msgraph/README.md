# <a name="how-to-run-the-completed-project"></a>完了したプロジェクトを実行する方法

## <a name="prerequisites"></a>前提条件

このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。

- 開発用のコンピューターにインストールされている[node.js](https://nodejs.org) 。 Node.js を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。 (**注:** このチュートリアルは、ノードバージョン10.15.3 を使用して作成されています。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)
- Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。

Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。

- [新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。
- [Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a>Web アプリケーションを Azure Active Directory 管理センターに登録する

1. ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)に移動します。 **個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。

1. 左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。

    ![アプリの登録のスクリーンショット ](/tutorial/images/aad-portal-app-registrations.png)

1. **[新規登録]** を選択します。 **[アプリケーションを登録]** ページで、次のように値を設定します。

    - `React Graph Tutorial` に **[名前]** を設定します。
    - **[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。
    - **[リダイレクト URI]** で、最初のドロップダウン リストを `Web` に設定し、それから `http://localhost:3000` に値を設定します。

    ![[アプリケーションの登録] ページのスクリーンショット](/tutorial/images/aad-register-an-app.png)

1. [**登録**] を選択します。 [**角度グラフのチュートリアル**] ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。次の手順で必要になります。

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

1. [**管理**] の下の [**認証**] を選択します。 暗黙的な**grant**セクションを見つけ、**アクセストークン**と**ID トークン**を有効にします。 **[保存]** を選択します。

    ![暗黙的な grant セクションのスクリーンショット](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a>サンプルを構成する

1. ファイルの`./graph-tutorial/src/Config.js.example`名前を`./graph-tutorial/src/Config.js`に変更します。
1. `./graph-tutorial/src/Config.js`ファイルを編集し、次のように変更します。
    1. を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。
1. コマンドラインインターフェイス (CLI) で、 `graph-tutorial`ディレクトリに移動し、次のコマンドを実行して要件をインストールします。

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a>サンプルを実行する

1. CLI で次のコマンドを実行して、アプリケーションを起動します。

    ```Shell
    npm start
    ```

1. Web ブラウザーを開き、`http://localhost:3000` を参照します。