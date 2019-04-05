<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="65c28-101">コマンドラインインターフェイス (CLI) を開き、ファイルを作成する権限があるディレクトリに移動し、次のコマンドを実行して、[アプリの作成](https://www.npmjs.com/package/create-react-app)ツールをインストールし、新しい反応アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="65c28-101">Open your command-line interface (CLI), navigate to a directory where you have rights to create files, and run the following commands to install the [create-react-app](https://www.npmjs.com/package/create-react-app) tool and create a new React app.</span></span>

```Shell
npm install create-react-app@2.1.5 -g
create-react-app graph-tutorial
```

<span data-ttu-id="65c28-102">コマンドが完了したら、CLI の`graph-tutorial`ディレクトリに移動し、次のコマンドを実行してローカル web サーバーを開始します。</span><span class="sxs-lookup"><span data-stu-id="65c28-102">Once the command finishes, change to the `graph-tutorial` directory in your CLI and run the following command to start a local web server.</span></span>

```Shell
npm start
```

<span data-ttu-id="65c28-103">既定のブラウザーが開き[https://localhost:3000/](https://localhost:3000) 、既定の反応ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="65c28-103">Your default browser opens to [https://localhost:3000/](https://localhost:3000) with a default React page.</span></span> <span data-ttu-id="65c28-104">ブラウザーが開かない場合は、それを開き、 [https://localhost:3000/](https://localhost:3000)を参照して、新しいアプリが動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="65c28-104">If your browser doesn't open, open it and browse to [https://localhost:3000/](https://localhost:3000) to verify that the new app works.</span></span>

<span data-ttu-id="65c28-105">に進む前に、後で使用する追加のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="65c28-105">Before moving on, install some additional packages that you will use later:</span></span>

- <span data-ttu-id="65c28-106">応答アプリケーション内の宣言型ルーティングのための[ルーター-dom](https://github.com/ReactTraining/react-router)を処理します。</span><span class="sxs-lookup"><span data-stu-id="65c28-106">[react-router-dom](https://github.com/ReactTraining/react-router) for declarative routing inside the React app.</span></span>
- <span data-ttu-id="65c28-107">スタイル設定と共通コンポーネントの[ブートストラップ](https://github.com/twbs/bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="65c28-107">[bootstrap](https://github.com/twbs/bootstrap) for styling and common components.</span></span>
- <span data-ttu-id="65c28-108">ブートストラップに基づくコンポーネントに対応するための[reactstrap](https://github.com/reactstrap/reactstrap) 。</span><span class="sxs-lookup"><span data-stu-id="65c28-108">[reactstrap](https://github.com/reactstrap/reactstrap) for React components based on Bootstrap.</span></span>
- <span data-ttu-id="65c28-109">アイコンの[fontawesome](https://github.com/FortAwesome/Font-Awesome) 。</span><span class="sxs-lookup"><span data-stu-id="65c28-109">[fontawesome-free](https://github.com/FortAwesome/Font-Awesome) for icons.</span></span>
- <span data-ttu-id="65c28-110">日付と時刻を書式設定するための[モーメント](https://github.com/moment/moment)。</span><span class="sxs-lookup"><span data-stu-id="65c28-110">[moment](https://github.com/moment/moment) for formatting dates and times.</span></span>
- <span data-ttu-id="65c28-111">Azure Active Directory に認証し、アクセストークンを取得するための[msal](https://github.com/AzureAD/microsoft-authentication-library-for-js) 。</span><span class="sxs-lookup"><span data-stu-id="65c28-111">[msal](https://github.com/AzureAD/microsoft-authentication-library-for-js) for authenticating to Azure Active Directory and retrieving access tokens.</span></span>
- <span data-ttu-id="65c28-112">[microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。</span><span class="sxs-lookup"><span data-stu-id="65c28-112">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to Microsoft Graph.</span></span>

<span data-ttu-id="65c28-113">CLI で次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="65c28-113">Run the following command in your CLI.</span></span>

```Shell
npm install react-router-dom@4.3.1 bootstrap@4.3.1 reactstrap@7.1.0 @fortawesome/fontawesome-free@5.7.2
npm install moment@2.24.0 msal@0.2.4 @microsoft/microsoft-graph-client@1.5.2
```

## <a name="design-the-app"></a><span data-ttu-id="65c28-114">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="65c28-114">Design the app</span></span>

<span data-ttu-id="65c28-115">最初に、アプリのナビゲーションバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="65c28-115">Start by creating a navbar for the app.</span></span> <span data-ttu-id="65c28-116">という名前`./src` `Navbar.js`のディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="65c28-116">Create a new file in the `./src` directory named `Navbar.js` and add the following code.</span></span>

```JSX
import React from 'react';
import { NavLink as RouterNavLink } from 'react-router-dom';
import {
  Collapse,
  Container,
  Navbar,
  NavbarToggler,
  NavbarBrand,
  Nav,
  NavItem,
  NavLink,
  UncontrolledDropdown,
  DropdownToggle,
  DropdownMenu,
  DropdownItem } from 'reactstrap';
import '@fortawesome/fontawesome-free/css/all.css';

function UserAvatar(props) {
  // If a user avatar is available, return an img tag with the pic
  if (props.user.avatar) {
    return <img
            src={props.user.avatar} alt="user"
            className="rounded-circle align-self-center mr-2"
            style={{width: '32px'}}></img>;
  }

  // No avatar available, return a default icon
  return <i
          className="far fa-user-circle fa-lg rounded-circle align-self-center mr-2"
          style={{width: '32px'}}></i>;
}

function AuthNavItem(props) {
  // If authenticated, return a dropdown with the user's info and a
  // sign out button
  if (props.isAuthenticated) {
    return (
      <UncontrolledDropdown>
        <DropdownToggle nav caret>
          <UserAvatar user={props.user}/>
        </DropdownToggle>
        <DropdownMenu right>
          <h5 className="dropdown-item-text mb-0">{props.user.displayName}</h5>
          <p className="dropdown-item-text text-muted mb-0">{props.user.email}</p>
          <DropdownItem divider />
          <DropdownItem onClick={props.authButtonMethod}>Sign Out</DropdownItem>
        </DropdownMenu>
      </UncontrolledDropdown>
    );
  }

  // Not authenticated, return a sign in link
  return (
    <NavItem>
      <NavLink onClick={props.authButtonMethod}>Sign In</NavLink>
    </NavItem>
  );
}

export default class NavBar extends React.Component {
  constructor(props) {
    super(props);

    this.toggle = this.toggle.bind(this);
    this.state = {
      isOpen: false
    };
  }

  toggle() {
    this.setState({
      isOpen: !this.state.isOpen
    });
  }

  render() {
    // Only show calendar nav item if logged in
    let calendarLink = null;
    if (this.props.isAuthenticated) {
      calendarLink = (
        <NavItem>
          <RouterNavLink to="/calendar" className="nav-link" exact>Calendar</RouterNavLink>
        </NavItem>
      );
    }

    return (
      <div>
        <Navbar color="dark" dark expand="md" fixed="top">
          <Container>
            <NavbarBrand href="/">React Graph Tutorial</NavbarBrand>
            <NavbarToggler onClick={this.toggle} />
            <Collapse isOpen={this.state.isOpen} navbar>
              <Nav className="mr-auto" navbar>
                <NavItem>
                  <RouterNavLink to="/" className="nav-link" exact>Home</RouterNavLink>
                </NavItem>
                {calendarLink}
              </Nav>
              <Nav className="justify-content-end" navbar>
                <NavItem>
                  <NavLink href="https://developer.microsoft.com/graph/docs/concepts/overview" target="_blank">
                    <i className="fas fa-external-link-alt mr-1"></i>
                    Docs
                  </NavLink>
                </NavItem>
                <AuthNavItem
                  isAuthenticated={this.props.isAuthenticated}
                  authButtonMethod={this.props.authButtonMethod}
                  user={this.props.user} />
              </Nav>
            </Collapse>
          </Container>
        </Navbar>
      </div>
    );
  }
}
```

<span data-ttu-id="65c28-117">次に、アプリのホームページを作成します。</span><span class="sxs-lookup"><span data-stu-id="65c28-117">Next, create a home page for the app.</span></span> <span data-ttu-id="65c28-118">という名前`./src` `Welcome.js`のディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="65c28-118">Create a new file in the `./src` directory named `Welcome.js` and add the following code.</span></span>

```JSX
import React from 'react';
import {
  Button,
  Jumbotron } from 'reactstrap';

function WelcomeContent(props) {
  // If authenticated, greet the user
  if (props.isAuthenticated) {
    return (
      <div>
        <h4>Welcome {props.user.displayName}!</h4>
        <p>Use the navigation bar at the top of the page to get started.</p>
      </div>
    );
  }

  // Not authenticated, present a sign in button
  return <Button color="primary" onClick={props.authButtonMethod}>Click here to sign in</Button>;
}

export default class Welcome extends React.Component {
  render() {
    return (
      <Jumbotron>
        <h1>React Graph Tutorial</h1>
        <p className="lead">
            This sample app shows how to use the Microsoft Graph API to access Outlook and OneDrive data from React
        </p>
        <WelcomeContent
          isAuthenticated={this.props.isAuthenticated}
          user={this.props.user}
          authButtonMethod={this.props.authButtonMethod} />
      </Jumbotron>
    );
  }
}
```

<span data-ttu-id="65c28-119">次に、エラーメッセージ表示を作成して、ユーザーにメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="65c28-119">Now create an error message display to display messages to the user.</span></span> <span data-ttu-id="65c28-120">という名前`./src` `ErrorMessage.js`のディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="65c28-120">Create a new file in the `./src` directory named `ErrorMessage.js` and add the following code.</span></span>

```JSX
import React from 'react';
import { Alert } from 'reactstrap';

export default class ErrorMessage extends React.Component {
  render() {
    let debug = null;
    if (this.props.debug) {
      debug = <pre className="alert-pre border bg-light p-2"><code>{this.props.debug}</code></pre>;
    }
    return (
      <Alert color="danger">
        <p className="mb-3">{this.props.message}</p>
        {debug}
      </Alert>
    );
  }
}
```

<span data-ttu-id="65c28-121">これらの基本コンポーネントが定義されたので、アプリを更新して使用します。</span><span class="sxs-lookup"><span data-stu-id="65c28-121">Now with those basic components defined, update the app to use them.</span></span> <span data-ttu-id="65c28-122">最初に、 `./src/index.css`ファイルを開き、その内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="65c28-122">First, open the `./src/index.css` file and replace its entire contents with the following.</span></span>

```css
body {
  padding-top: 4.5rem;
}

.alert-pre {
  word-wrap: break-word;
  word-break: break-all;
  white-space: pre-wrap;
}
```

<span data-ttu-id="65c28-123">次に、 `./src/App.js`を開いて、コンテンツ全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="65c28-123">Next, open `./src/App.js` and replace its entire contents with the following.</span></span>

```JSX
import React, { Component } from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import { Container } from 'reactstrap';
import NavBar from './NavBar';
import ErrorMessage from './ErrorMessage';
import Welcome from './Welcome';
import 'bootstrap/dist/css/bootstrap.css';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      isAuthenticated: false,
      user: {},
      error: null
    };
  }

  render() {
    let error = null;
    if (this.state.error) {
      error = <ErrorMessage message={this.state.error.message} debug={this.state.error.debug} />;
    }

    return (
      <Router>
        <div>
          <NavBar
            isAuthenticated={this.state.isAuthenticated}
            authButtonMethod={null}
            user={this.state.user}/>
          <Container>
            {error}
            <Route exact path="/"
              render={(props) =>
                <Welcome {...props}
                  isAuthenticated={this.state.isAuthenticated}
                  user={this.state.user}
                  authButtonMethod={null} />
              } />
          </Container>
        </div>
      </Router>
    );
  }

  setErrorMessage(message, debug) {
    this.setState({
      error: {message: message, debug: debug}
    });
  }
}

export default App;
```

<span data-ttu-id="65c28-124">すべての変更を保存し、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="65c28-124">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="65c28-125">この時点で、アプリの外観は大きく異なります。</span><span class="sxs-lookup"><span data-stu-id="65c28-125">Now, the app should look very different.</span></span>

![再設計されたホームページのスクリーンショット](images/create-app-01.png)