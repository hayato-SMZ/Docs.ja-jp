---
title: ASP.NET Core での部分ビュー
author: ardalis
description: 部分ビューが別のビュー内でどのようにレンダリングされるビューか、ASP.NET Core アプリでどのような場合に使用すべきかについて説明します。
manager: wpickett
ms.author: riande
ms.date: 03/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/partial
ms.openlocfilehash: 3deaaeb666e5443d0784f2ac6977e58e1b25d711
ms.sourcegitcommit: 71b93b42cbce8a9b1a12c4d88391e75a4dfb6162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2018
ms.locfileid: "30000903"
---
# <a name="partial-views-in-aspnet-core"></a>ASP.NET Core での部分ビュー

作成者: [Steve Smith](https://ardalis.com/)、[Maher JENDOUBI](https://twitter.com/maherjend)、[Rick Anderson](https://twitter.com/RickAndMSFT)、[Scott Sauber](https://twitter.com/scottsauber)

ASP.NET Core MVC では部分ビューがサポートされます。これらのビューは、さまざまなビューで共有する Web ページの一部を再利用できる場合に便利です。

[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample)します ([ダウンロード方法](xref:tutorials/index#how-to-download-a-sample))。

## <a name="what-are-partial-views"></a>部分ビューとは

部分ビューとは、別のビュー内でレンダリングされるビューのことです。 部分ビューを実行して生成される HTML 出力は、呼び出し元 (または親) のビューにレンダリングされます。 ビューと同様、部分ビューでは *.cshtml* ファイル拡張子を使用します。

## <a name="when-should-i-use-partial-views"></a>部分ビューを使用する必要があるタイミング

部分ビューは、より小さい要素に大きいビューを分割する効果的な方法です。 ビュー コンテンツの重複を減らし、ビュー要素を再利用できます。 一般的なレイアウト要素は、[_Layout.cshtml](layout.md) に指定する必要があります。 レイアウト以外の再利用可能なコンテンツは、部分ビューにカプセル化できます。

いくつかの論理部分で構成される複雑なページがある場合、それぞれの部分を独自の部分ビューとして操作する際に役立ちます。 ページの各部分はページの残りの部分とは別に表示でき、ページ自体のビューははるかに単純になります。これは、部分ビューをレンダリングするための呼び出しとページ構造全体のみが含まれるためです。

ヒント: ビューでは [DRY 原則](http://deviq.com/don-t-repeat-yourself/)に従ってください。

## <a name="declaring-partial-views"></a>部分ビューの宣言

部分ビューは他のビューと同様に作成されます。その場合、*Views* フォルダー内に *.cshtml* ファイルを作成します。 部分ビューと標準ビューのセマンティックに違いはありません。ただ、レンダリングの方法が異なるだけです。 コントローラーの `ViewResult` から直接返されるビューを使用でき、これと同じビューを部分ビューとして使用できます。 ビューと部分ビューのレンダリング方法の主な違いは、部分ビューでは *_ViewStart.cshtml* を実行しないことです (ビューでは実行します。詳細については、「[レイアウト](layout.md)」の *_ViewStart.cshtml* に関する記述を参照してください)。

## <a name="referencing-a-partial-view"></a>部分ビューの参照

ビュー ページ内から、部分ビューをレンダリングできる方法がいくつかあります。 ベスト プラクティスは、`Html.PartialAsync` を使用することです。この場合、`IHtmlString` を返し、呼び出しの前に `@` を指定して参照できます。

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=8)]

`RenderPartialAsync` を使用して、部分ビューをレンダリングできます。 このメソッドは結果を返しません。レンダリングされた出力を直接応答にストリーミングします。 結果を返さないため、Razor コード ブロック内で呼び出す必要があります。

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=11-13)]

結果を直接ストリーミングするため、一部のシナリオでは `RenderPartialAsync` のパフォーマンスが向上する場合がありますが、 `PartialAsync` を使用することをお勧めします。

`Html.PartialAsync` (`Html.Partial`) と `Html.RenderPartialAsync` (`Html.RenderPartial`) という同期相当の機能がありますが、デッドロックが発生するシナリオがあるため、同期相当の機能の使用はお勧めしません。 今後のバージョンでは、この同期方法は使用されなくなる予定です。

> [!NOTE]
> ビューでコードを実行する必要がある場合は、部分ビューの代わりに[ビュー コンポーネント](view-components.md)を使用するパターンをお勧めします。

### <a name="partial-view-discovery"></a>部分ビューの検出

部分ビューを参照するときに、いくつかの方法でその場所を参照することができます。

```cshtml
// Uses a view in current folder with this name
// If none is found, searches the Shared folder
@await Html.PartialAsync("ViewName")

// A view with this name must be in the same folder
@await Html.PartialAsync("ViewName.cshtml")

// Locate the view based on the application root
// Paths that start with "/" or "~/" refer to the application root
@await Html.PartialAsync("~/Views/Folder/ViewName.cshtml")
@await Html.PartialAsync("/Views/Folder/ViewName.cshtml")

// Locate the view using relative paths
@await Html.PartialAsync("../Account/LoginPartial.cshtml")
```

別のビュー フォルダーで同じ名前の別の部分ビューを使用することができます。 名前 (ファイル拡張子なし) でビューを参照する場合、各フォルダー内のビューではそれと同じフォルダーの部分ビューを使用します。 *Shared* フォルダーに配置して、使用する既定の部分ビューを指定することもできます。 共有部分ビューは、部分ビューの独自のバージョンがないすべてのビューで使用されます。 親ビューと同じフォルダーの同じ名前の部分ビューによってオーバーライドされる、既定の部分ビューを (*Shared* 内で) 使用できます。

部分ビューを*チェーンする*ことができます。 つまり、部分ビューは別の部分ビューを呼び出すことができます (ただし、ループを作成しない場合)。 各ビューまたは部分ビュー内では、相対パスは、ルートや親ビューではなく、常にそのビューに対して相対的になります。

> [!NOTE]
> 部分ビューで [Razor](razor.md) `section` を宣言すると、その親に表示されなくなります。これは親ビューに限定されます。

## <a name="accessing-data-from-partial-views"></a>部分ビューからのデータへのアクセス

親ビューのインスタンス化の際に、親ビューの `ViewData` ディクショナリのコピーが取得されます。 親ビュー内のデータに対して行われた更新は、親ビューでは保持されません。 部分ビューで変更された `ViewData` は、部分ビューから返されるときに失われます。

`ViewDataDictionary` のインスタンスを部分ビューに渡すことができます。

```cshtml
@await Html.PartialAsync("PartialName", customViewData)
```

部分ビューにモデルを渡すこともできます。 これは、ページのビュー モデルまたはカスタム オブジェクトの場合があります。 モデルを `PartialAsync` または `RenderPartialAsync` に渡すことができます。

```cshtml
@await Html.PartialAsync("PartialName", viewModel)
```

`ViewDataDictionary` のインスタンスとビュー モデルを部分ビューに渡すことができます。

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml?range=15-16)]

以下のマークアップは、2 つの部分ビューを含む *Views/Articles/Read.cshtml* ビューを示しています。 2 番目の部分ビューは、モデルと `ViewData` を部分ビューに渡します。 以下の強調表示されている `ViewDataDictionary` のコンストラクター オーバーロードを使用する場合、既存の `ViewData` を維持したまま、新しい `ViewData` ディクショナリを渡すことができます。

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml)]

*Views/Shared/AuthorPartial*:

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Shared/AuthorPartial.cshtml)]

*ArticleSection* 部分:

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/ArticleSection.cshtml)]

実行時に、この部分は親ビューにレンダリングされます。親ビュー自体は共有されている *_Layout.cshtml* 内にレンダリングされます。

![部分ビューの出力](partial/_static/output.png)
