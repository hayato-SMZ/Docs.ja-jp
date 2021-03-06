---
title: ASP.NET Core と Visual Studio for Windows で Web API を作成する
author: rick-anderson
description: ASP.NET Core MVC と Visual Studio for Windows で Web API を構築する
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
uid: tutorials/first-web-api
ms.openlocfilehash: 3da22cbbbe0db7771656997a13587521e182fb2a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277401"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a>ASP.NET Core と Visual Studio for Windows で Web API を作成する

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT) と [Mike Wasson](https://github.com/mikewasson)

このチュートリアルでは、"to-do" 項目の一覧を管理する Web API を構築します。 ユーザー インターフェイス (UI) は作成されません。

このチュートリアルには 3 つのバージョンがあります。

* Windows: Visual Studio for Windows で Web API を作成する (このチュートリアル)
* macOS: [Visual Studio for Mac で Web API を作成する](xref:tutorials/first-web-api-mac)
* macOS、Linux、Windows: [Visual Studio Code で Web API を作成する](xref:tutorials/web-api-vsc)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a>必須コンポーネント

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a>プロジェクトの作成

Visual Studio で次の手順を実行します。

* **[ファイル]** メニューで、**[新規作成]**、**[プロジェクト]** の順に作成します。
* **[ASP.NET Core Web アプリケーション]** テンプレートを選択します。 プロジェクトに「*TodoApi*」という名前を付け、**[OK]** をクリックます。
* **[New ASP.NET Core Web Application - TodoApi]\(新しい ASP.NET Core Web アプリケーション - TodoApi\)** ダイアログで、ASP.NET Core のバージョンを選択します。 **API** テンプレートを選択し、**[OK]** をクリックします。 **[Enable Docker Support]\(Docker サポートを有効にする\)** は**選択しないで**ください。

### <a name="launch-the-app"></a>アプリの起動

Visual Studio で、CTRL を押しながら F5 を押し、アプリを起動します。 Visual Studio でブラウザーが起動し、`http://localhost:<port>/api/values` にアクセスします。ここで、`<port>` はランダムに選択されたポート番号になります。 Chrome、Microsoft Edge、Firefox では次の出力が表示されます。

```json
["value1","value2"]
```

Internet Explorer を使っている場合、*values.json* ファイルを保存するように求められます。

### <a name="add-a-model-class"></a>モデル クラスの追加

モデルは、アプリのデータを表すオブジェクトです。 ここでは、唯一のモデルが to-do 項目です。

ソリューション エクスプローラーで、プロジェクトを右クリックします。 **[追加]** > **[新しいフォルダー]** の順に選択します。 フォルダーに *Models* という名前を付けます。

> [!NOTE]
> モデル クラスはプロジェクト内のどこでも使用できます。 通例として、モデル クラス用に *Models* フォルダーを使用しています。

ソリューション エクスプローラーで、*[Models]* フォルダーを右クリックし、**[追加]**、**[クラス]** の順に選択します。 クラスに「*TodoItem*」という名前を付け、**[追加]** をクリックします。

`TodoItem` クラスを次のコードで更新します。

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

`TodoItem` が作成されるとき、データベースは `Id` を生成します。

### <a name="create-the-database-context"></a>データベース コンテキストの作成

*データベース コンテキスト*は、所与のデータ モデルに対し、Entity Framework 機能を調整するメイン クラスです。 このクラスは `Microsoft.EntityFrameworkCore.DbContext` クラスから派生させて作成します。

ソリューション エクスプローラーで、*[Models]* フォルダーを右クリックし、**[追加]**、**[クラス]** の順に選択します。 クラスに「*TodoContext*」という名前を付け、**[追加]** をクリックします。

このクラスを次のコードで置き換えます。

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a>コントローラーの追加

ソリューション エクスプローラーで、*Controllers* フォルダーを右クリックします。 **[追加]** > **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、**[API コントローラー クラス]** テンプレートを選択します。 クラスに「*TodoController*」という名前を付け、**[追加]** をクリックします。

![[新しい項目の追加] ダイアログ。検索ボックスに「controller」と入力されています。Web API コントローラーが選択されています。](first-web-api/_static/new_controller.png)

このクラスを次のコードで置き換えます。

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>アプリの起動

Visual Studio で、CTRL を押しながら F5 を押し、アプリを起動します。 Visual Studio でブラウザーが起動し、`http://localhost:<port>/api/values` にアクセスします。ここで、`<port>` はランダムに選択されたポート番号になります。 `http://localhost:<port>/api/todo` の `Todo` コントローラーに移動します。

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
