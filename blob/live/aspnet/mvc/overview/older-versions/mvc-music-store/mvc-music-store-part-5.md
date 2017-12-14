---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: "手順 5: 編集フォームやテンプレート |Microsoft ドキュメント"
author: jongalloway
description: "このチュートリアルの系列では、すべての ASP.NET MVC Music Store サンプル アプリケーションをビルドする手順について説明します。 パート 5 は、編集フォームとテンプレートについて説明します。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: cde6fe133291254531a797a434a4b2cdd226dd5f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
<a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="99465-104">手順 5: 編集フォームとテンプレート</span><span class="sxs-lookup"><span data-stu-id="99465-104">Part 5: Edit Forms and Templating</span></span>
====================
<span data-ttu-id="99465-105">によって[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="99465-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="99465-106">MVC Music Store は、チュートリアル アプリケーションを紹介し、ASP.NET MVC と Visual Studio web 開発を使用する方法の詳細な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="99465-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="99465-107">MVC 音楽ストアは、オンラインにして、音楽のアルバムを販売し、基本的なサイトの管理、ユーザー サインインおよび買い物カゴの機能を実装する軽量なサンプル ストアの実装です。</span><span class="sxs-lookup"><span data-stu-id="99465-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="99465-108">このチュートリアルの系列では、すべての ASP.NET MVC Music Store サンプル アプリケーションをビルドする手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="99465-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="99465-109">パート 5 は、編集フォームとテンプレートについて説明します。</span><span class="sxs-lookup"><span data-stu-id="99465-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="99465-110">過去の章では、データベースからデータを読み込むと、表示するおされました。</span><span class="sxs-lookup"><span data-stu-id="99465-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="99465-111">この章でも、データの編集を有効にしています。</span><span class="sxs-lookup"><span data-stu-id="99465-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="99465-112">StoreManagerController を作成します。</span><span class="sxs-lookup"><span data-stu-id="99465-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="99465-113">まずと呼ばれる新しいコント ローラーの作成、 **StoreManagerController**です。</span><span class="sxs-lookup"><span data-stu-id="99465-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="99465-114">このコント ローラーで取得 ASP.NET MVC 3 Tools Update で利用できるスキャフォールディング機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="99465-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="99465-115">次に示すように、コント ローラーの追加 ダイアログのオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="99465-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="99465-116">[追加] ボタンをクリックすると、ASP.NET MVC 3 のスキャフォールディング機構は、十分な量の作業が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="99465-117">Entity Framework のローカル変数を新しい StoreManagerController に作成されます。</span><span class="sxs-lookup"><span data-stu-id="99465-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="99465-118">StoreManager フォルダー、プロジェクトのビュー フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="99465-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="99465-119">アルバム クラスを厳密に型指定された Create.cshtml、Delete.cshtml、Details.cshtml、Edit.cshtml、および Index.cshtml のビューを追加します。</span><span class="sxs-lookup"><span data-stu-id="99465-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="99465-120">新しい StoreManager コント ローラー クラスには、CRUD (作成、読み取り、更新、削除)、アルバムを操作する方法を知っているコント ローラーのアクションがモデル クラスとデータベース アクセスに対して、Entity Framework コンテキストを使用します。</span><span class="sxs-lookup"><span data-stu-id="99465-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="99465-121">スキャフォールディング ビューを変更します。</span><span class="sxs-lookup"><span data-stu-id="99465-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="99465-122">ことが重要うえで、このコードが生成された、ときに、このチュートリアル全体での執筆と同じように、標準の ASP.NET MVC コードがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="99465-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="99465-123">定型的なコント ローラーのコードを記述し、厳密に型指定されたビューを手動で作成するのには、時間を保存するためのものしますが、不吉な警告に照準を変更する方法についてのコメントで始まるみたことがある生成されたコードの種類はありません、コードです。</span><span class="sxs-lookup"><span data-stu-id="99465-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="99465-124">これは、コードであり、変更する必要が。</span><span class="sxs-lookup"><span data-stu-id="99465-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="99465-125">そのため、クイック編集 StoreManager インデックス ビューを使用して開始しましょう (/Views/StoreManager/Index.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="99465-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="99465-126">このビューは、ストア内で編集のアルバムの一覧を表示するテーブルを表示//リンクの削除を詳細アルバムのパブリック プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="99465-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="99465-127">AlbumArtUrl フィールドに、この表示で非常に効果的ではなく、削除されます。</span><span class="sxs-lookup"><span data-stu-id="99465-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="99465-128">&lt;テーブル&gt;セクション コードの表示 の削除、 &lt;th&gt;と&lt;td&gt;以下の強調表示された行が示すとおり、AlbumArtUrl 参照を囲む要素。</span><span class="sxs-lookup"><span data-stu-id="99465-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="99465-129">コードの変更の表示は、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="99465-130">ストア マネージャーで最初に表示</span><span class="sxs-lookup"><span data-stu-id="99465-130">A first look at the Store Manager</span></span>

<span data-ttu-id="99465-131">ここで、アプリケーションを実行し、/StoreManager を参照します。</span><span class="sxs-lookup"><span data-stu-id="99465-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="99465-132">これには、格納マネージャーのインデックスが変更、編集、詳細、および削除へのリンクを使用してストアのアルバムの一覧を表示が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="99465-133">[編集] リンクをクリックすると、アルバム、ジャンル、アーティストのドロップダウン リストを含むフィールドの編集フォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="99465-134">下部で、「リストに戻る」リンクをクリックし、アルバムの詳細 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="99465-135">これには、個々 のアルバムの詳細情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="99465-136">もう一度、一覧のリンクに戻る をクリックし、削除 リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="99465-137">これには、アルバムの詳細を表示し、それを削除することを確認しているかを確認する、確認ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="99465-138">下部にある [削除] ボタンをクリックすると、アルバムの削除し、削除アルバムを表示するインデックス ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="99465-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="99465-139">ストア マネージャーで終わっていませんがが動作しているコント ローラーおよびからを起動する CRUD 操作のコードの表示。</span><span class="sxs-lookup"><span data-stu-id="99465-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="99465-140">ストア マネージャー コント ローラーのコードを見る</span><span class="sxs-lookup"><span data-stu-id="99465-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="99465-141">ストア マネージャー コント ローラーには、十分な量コードにはが含まれています。</span><span class="sxs-lookup"><span data-stu-id="99465-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="99465-142">みましょうこの上から下にします。</span><span class="sxs-lookup"><span data-stu-id="99465-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="99465-143">コント ローラーには、ある MVC コント ローラーだけでなく、モデルの名前空間への参照の一部の標準的な名前空間が含まれています。</span><span class="sxs-lookup"><span data-stu-id="99465-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="99465-144">コント ローラーは、データ アクセス用の各コント ローラー アクションで使用されている MusicStoreEntities のプライベート インスタンスを持ちます。</span><span class="sxs-lookup"><span data-stu-id="99465-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="99465-145">ストア マネージャーのインデックスと詳細の操作</span><span class="sxs-lookup"><span data-stu-id="99465-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="99465-146">インデックス ビューは、アルバム、情報を含む各アルバムの参照先ジャンル、アーティスト以前見たようストア参照メソッドを使用する場合の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="99465-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="99465-147">インデックス ビューが効率を実現し、元の要求にこの情報の照会、コント ローラーが表示されるように各アルバムのジャンル名、アーティスト名、表示できるように後は、リンクされたオブジェクトへの参照に制限します。</span><span class="sxs-lookup"><span data-stu-id="99465-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="99465-148">StoreManager コント ローラーのコント ローラー アクションの詳細とまったく同じ動作に書いた以前のアルバムの問い合わせストア コント ローラーの詳細アクションとして Find() メソッドを使用して ID を使用して、ビューに戻ることです。</span><span class="sxs-lookup"><span data-stu-id="99465-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="99465-149">アクション メソッドを作成</span><span class="sxs-lookup"><span data-stu-id="99465-149">The Create Action Methods</span></span>

<span data-ttu-id="99465-150">アクション メソッドを作成するは、フォーム入力を処理するためにここまでは、見たものとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="99465-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="99465-151">ユーザーが初めてアクセス/StoreManager/作成/それらが表示されます、空のフォーム。</span><span class="sxs-lookup"><span data-stu-id="99465-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="99465-152">この HTML ページには、&lt;フォーム&gt;をドロップダウン リストとテキスト ボックスを含む要素の入力要素のアルバムの詳細を入力することができます。</span><span class="sxs-lookup"><span data-stu-id="99465-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="99465-153">アルバムのフォーム値に入力した後は、これらの変更がデータベース内で保存するようにアプリケーションに戻す [保存] ボタンを押して、ことができます。</span><span class="sxs-lookup"><span data-stu-id="99465-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="99465-154">ユーザーが [保存] ボタンを押したとき、&lt;フォーム&gt;/StoreManager/作成/URL に HTTP POST を実行し、送信、&lt;フォーム&gt;HTTP POST の一部として値。</span><span class="sxs-lookup"><span data-stu-id="99465-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="99465-155">ASP.NET MVC では、–、/StoreManager/Create を初期の HTTP GET 参照を処理する 1 つ、StoreManagerController クラス内で 2 つ別々 の「作成」操作メソッドを実装することを有効にすると、これら 2 つの URL 呼び出しシナリオのロジックを簡単に分割することができます。/URL、および、その他の送信された変更の HTTP POST を処理します。</span><span class="sxs-lookup"><span data-stu-id="99465-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="99465-156">ViewBag を使用してビューに情報を渡す.</span><span class="sxs-lookup"><span data-stu-id="99465-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="99465-157">このチュートリアルで先ほど ViewBag を使用したしましたが多くについて説明します。</span><span class="sxs-lookup"><span data-stu-id="99465-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="99465-158">ViewBag を使用して、厳密に型指定されたモデル オブジェクトを使用せず、ビューに情報を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="99465-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="99465-159">ここで、編集の HTTP GET コント ローラーのアクションをドロップダウン リストを作成するフォームに両方のジャンル、アーティストの一覧を渡す必要がありますを行うには最も簡単な方法 ViewBag 項目として値を返すにします。</span><span class="sxs-lookup"><span data-stu-id="99465-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="99465-160">ViewBag は動的オブジェクトでは、これらのプロパティを定義するコードを記述することがなく ViewBag.Foo または ViewBag.YourNameHere を入力できます。</span><span class="sxs-lookup"><span data-stu-id="99465-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="99465-161">この場合、コント ローラーのコードを使用して ViewBag.GenreId と ViewBag.ArtistId GenreId と ArtistId、アルバムのプロパティの設定を行うには、フォームの送信 ドロップダウンの値ができるようにします。</span><span class="sxs-lookup"><span data-stu-id="99465-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="99465-162">目的にのみ構築された SelectList オブジェクトを使用してフォームには、これらのドロップダウン リストの値が返されます。</span><span class="sxs-lookup"><span data-stu-id="99465-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="99465-163">これは、次のようにコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="99465-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="99465-164">アクション メソッドのコードからわかるように、このオブジェクトを作成する 3 つのパラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="99465-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="99465-165">ドロップダウン リストが表示されている項目の一覧。</span><span class="sxs-lookup"><span data-stu-id="99465-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="99465-166">これは単なる文字列 - ジャンルの一覧を渡していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="99465-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="99465-167">次に、SelectList に渡されるパラメーターは、選択した値です。</span><span class="sxs-lookup"><span data-stu-id="99465-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="99465-168">この方法、SelectList は、リスト内の項目を事前に選択する方法を認識しています。</span><span class="sxs-lookup"><span data-stu-id="99465-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="99465-169">非常に類似した編集フォームに詳しく見てみるとわかりやすくなります。</span><span class="sxs-lookup"><span data-stu-id="99465-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="99465-170">最後のパラメーターは、表示されるプロパティです。</span><span class="sxs-lookup"><span data-stu-id="99465-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="99465-171">この場合、Genre.Name プロパティがユーザーに表示される内容を示すこのです。</span><span class="sxs-lookup"><span data-stu-id="99465-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="99465-172">念頭に、HTTP GET 作成操作は非常に単純な - SelectLists の 2 つは、ViewBag に追加し、モデル オブジェクトが渡されないフォーム (まだ作成されていない) からします。</span><span class="sxs-lookup"><span data-stu-id="99465-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="99465-173">ビューの作成で、ドロップ ダウンを表示する HTML ヘルパー</span><span class="sxs-lookup"><span data-stu-id="99465-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="99465-174">ビューに、ドロップダウンの値を渡す方法について説明した、ためそれらの値を表示する方法を表示するビューを簡単に見てをみましょう。</span><span class="sxs-lookup"><span data-stu-id="99465-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="99465-175">コードの表示で (/Views/StoreManager/Create.cshtml)、ジャンル ボックスの一覧を表示する次の呼び出しが行われたわかりますダウンします。</span><span class="sxs-lookup"><span data-stu-id="99465-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="99465-176">これは、HTML ヘルパーの一般的なタスクの表示を実行するユーティリティ メソッドと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="99465-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="99465-177">HTML ヘルパーは簡潔で読みやすく、コードの表示を維持するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="99465-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="99465-178">Html.DropDownList ヘルパーは、ASP.NET MVC によって提供されるが、後でおわかりのよう、アプリケーションで再利用してコードの表示に独自のヘルパーを作成すること。</span><span class="sxs-lookup"><span data-stu-id="99465-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="99465-179">Html.DropDownList 呼び出しだけおく必要があります次の 2 つの場所を get 一覧表示するにはどのような値 (存在する場合) があらかじめ選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99465-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="99465-180">GenreId、最初のパラメーターは、モデルまたは ViewBag GenreId をという名前の値を検索する DropDownList を指示します。</span><span class="sxs-lookup"><span data-stu-id="99465-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="99465-181">2 番目のパラメーターは、ドロップダウン リストで最初に、選択を表示する値を示すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="99465-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="99465-182">このフォームがフォームを作成するためは、あらかじめ選択されている値はありません、String.Empty が渡されます。</span><span class="sxs-lookup"><span data-stu-id="99465-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="99465-183">フォームのポストされた値の処理</span><span class="sxs-lookup"><span data-stu-id="99465-183">Handling the Posted Form values</span></span>

<span data-ttu-id="99465-184">前に説明したよう各フォームに関連付けられている 2 つのアクション メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="99465-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="99465-185">1 つ目は、HTTP GET 要求を処理し、フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="99465-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="99465-186">2 つ目は、送信されたフォーム値を含む HTTP POST 要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="99465-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="99465-187">コント ローラーのアクションが HTTP POST 要求に応答する必要がありますのみ ASP.NET MVC に指示する、[HttpPost] 属性を持つことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="99465-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="99465-188">この操作には、次の 4 つの責任があります。</span><span class="sxs-lookup"><span data-stu-id="99465-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="99465-189">フォームの値を読み取る</span><span class="sxs-lookup"><span data-stu-id="99465-189">Read the form values</span></span>
- 2. <span data-ttu-id="99465-190">フォームの値がその検証ルールを渡すかどうかの確認します。</span><span class="sxs-lookup"><span data-stu-id="99465-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="99465-191">フォームの送信が有効な場合は、データを保存し、更新されたリストを表示</span><span class="sxs-lookup"><span data-stu-id="99465-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="99465-192">フォームの送信が有効でない場合は、検証エラーを含むフォームを再表示します</span><span class="sxs-lookup"><span data-stu-id="99465-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="99465-193">モデル バインディングでのフォーム値の読み取り</span><span class="sxs-lookup"><span data-stu-id="99465-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="99465-194">コント ローラーのアクションはタイトル、価格、および AlbumArtUrl GenreId および ArtistId (、ドロップダウン リストから) 値およびテキスト ボックスの値を含むフォームの送信を処理しています。</span><span class="sxs-lookup"><span data-stu-id="99465-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="99465-195">フォームの値に直接アクセスすることはできますより適切な方法では、ASP.NET MVC に組み込まれているモデル バインド機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="99465-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="99465-196">コント ローラーのアクションは、モデルの型をパラメーターとして受け取り、ASP.NET MVC はフォーム入力 (およびそのルートおよびクエリ文字列の値) を使用してその型のオブジェクトを設定しようとします。</span><span class="sxs-lookup"><span data-stu-id="99465-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="99465-197">これは、名前に一致するモデル オブジェクトのプロパティなどの値を探してで新しいアルバム オブジェクトの GenreId 値を設定するには、検索 GenreId の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="99465-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="99465-198">ASP.NET MVC での標準メソッドを使用して、ビューを作成するときに、フォームは常にレンダリングされますフィールドの名前だけが照合されますので、プロパティ名を使用して入力フィールド名として。</span><span class="sxs-lookup"><span data-stu-id="99465-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="99465-199">モデルの検証</span><span class="sxs-lookup"><span data-stu-id="99465-199">Validating the Model</span></span>

<span data-ttu-id="99465-200">ModelState.IsValid を単純な呼び出しでは、モデルが検証されます。</span><span class="sxs-lookup"><span data-stu-id="99465-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="99465-201">任意の検証規則、アルバム クラスに追加していないまだ - ビット - ため今すぐこのチェックはありませんはあまりすることによって行います。</span><span class="sxs-lookup"><span data-stu-id="99465-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="99465-202">重要な点は、この ModelStat.IsValid チェックは、検証規則に将来の変更は、コント ローラーのアクション コードへの更新を必要としないので、モデルの配置、検証規則に適用されます。</span><span class="sxs-lookup"><span data-stu-id="99465-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="99465-203">送信された値を保存します。</span><span class="sxs-lookup"><span data-stu-id="99465-203">Saving the submitted values</span></span>

<span data-ttu-id="99465-204">フォームの送信には、検証が成功した場合、値をデータベースに保存する時間を勧めします。</span><span class="sxs-lookup"><span data-stu-id="99465-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="99465-205">で Entity Framework、アルバム コレクションにモデルを追加して、SaveChanges を呼び出すことが必要です。</span><span class="sxs-lookup"><span data-stu-id="99465-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="99465-206">Entity Framework には、値を保存する適切な SQL コマンドが生成されます。</span><span class="sxs-lookup"><span data-stu-id="99465-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="99465-207">データを保存した後おアルバムの一覧に戻るようにリダイレクトは、更新プログラムを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99465-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="99465-208">これは、ここに表示するコント ローラー アクションの名前を持つ RedirectToAction を返すことによって行います。</span><span class="sxs-lookup"><span data-stu-id="99465-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="99465-209">この場合、インデックス メソッドです。</span><span class="sxs-lookup"><span data-stu-id="99465-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="99465-210">検証エラーを含む無効なフォームの送信を表示します。</span><span class="sxs-lookup"><span data-stu-id="99465-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="99465-211">場合は、入力の形式が無効です (HTTP GET 以外の場合) と同じ ViewBag にドロップダウン リストの値を追加および表示用のビューにバインドされたモデルの値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="99465-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="99465-212">検証エラーが自動的に表示されるを使用して、 @Html.ValidationMessageFor HTML ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="99465-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="99465-213">テスト フォームを作成します。</span><span class="sxs-lookup"><span data-stu-id="99465-213">Testing the Create Form</span></span>

<span data-ttu-id="99465-214">これをテストするには、実行/StoreManager/作成/- を参照しをアプリケーションが表示されます、StoreController 作成 HTTP-GET メソッドによって返されたを空白のフォーム。</span><span class="sxs-lookup"><span data-stu-id="99465-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="99465-215">いくつかの値を入力し、フォームを送信する作成ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="99465-216">編集の処理</span><span class="sxs-lookup"><span data-stu-id="99465-216">Handling Edits</span></span>

<span data-ttu-id="99465-217">編集操作のペア (HTTP-GET および HTTP-POST) は、お見ただけでアクション メソッドを作成するとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="99465-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="99465-218">編集シナリオでは、既存のアルバム、編集 HTTP の GET メソッドは、"id"パラメーターに基づくアルバムを読み込みます。 操作のために経由で渡されたルート。</span><span class="sxs-lookup"><span data-stu-id="99465-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="99465-219">AlbumId のアルバムを取得するためには、このコードは、詳細のコント ローラー アクションでを見てみました以前と同じです。</span><span class="sxs-lookup"><span data-stu-id="99465-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="99465-220">作成と同様に HTTP GET メソッドで、ドロップダウンの値は、ViewBag を介して返されます。/です。</span><span class="sxs-lookup"><span data-stu-id="99465-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="99465-221">これにより、モデル オブジェクトとして (これは厳密に型指定されたアルバム クラス) ビューにアルバムを返す ViewBag を使用して追加のデータ (例: ジャンルの一覧) を渡す際にできます。</span><span class="sxs-lookup"><span data-stu-id="99465-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="99465-222">編集の HTTP POST 操作では、作成の HTTP POST 操作によく似ています。</span><span class="sxs-lookup"><span data-stu-id="99465-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="99465-223">唯一の違いは、db に新しいアルバムを追加する代わりにします。アルバム コレクションおを進めて、アルバムの現在のインスタンス db を使用します。Entry(album) および modified 状態に設定します。</span><span class="sxs-lookup"><span data-stu-id="99465-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="99465-224">これにより、Entity Framework 新規に作成するのではなく既存のアルバムを変更することがなります。</span><span class="sxs-lookup"><span data-stu-id="99465-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="99465-225">この出力は、アプリケーションの実行/StoreManger/を参照し、アルバムの編集リンクをクリックすると、おテストできます。</span><span class="sxs-lookup"><span data-stu-id="99465-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="99465-226">これには、編集の HTTP GET メソッドで表示される編集フォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="99465-227">いくつかの値を入力し、[保存] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="99465-228">フォームをポストこの、値を保存し、アルバム リストに値が更新されたことを示す us を返します。</span><span class="sxs-lookup"><span data-stu-id="99465-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="99465-229">削除の処理</span><span class="sxs-lookup"><span data-stu-id="99465-229">Handling Deletion</span></span>

<span data-ttu-id="99465-230">削除では、編集および作成する、確認フォームを表示する 1 つのコント ローラーのアクションとフォームの送信を処理する別のコント ローラー アクションを使用すると同様のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="99465-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="99465-231">コント ローラーの HTTP GET Delete アクションは、以前のストア マネージャーの詳細コント ローラーのアクションとまったくです。</span><span class="sxs-lookup"><span data-stu-id="99465-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="99465-232">私たちは、削除ビューのコンテンツ テンプレートを使用して、アルバムの型に厳密に型指定されたフォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="99465-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="99465-233">そのダウンを少しお簡略化できますが、削除のテンプレートには、モデルのすべてのフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="99465-234">/Views/StoreManager/Delete.cshtml でコードの表示を次に変更します。</span><span class="sxs-lookup"><span data-stu-id="99465-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="99465-235">これには、簡略化された削除の確認が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="99465-236">DeleteConfirmed アクションを実行すると、サーバーに送り返すにフォームと削除 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="99465-237">HTTP POST 削除コント ローラーのアクションは、次のアクションを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="99465-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="99465-238">ID でアルバムを読み込みます</span><span class="sxs-lookup"><span data-stu-id="99465-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="99465-239">アルバムを削除し、変更を保存</span><span class="sxs-lookup"><span data-stu-id="99465-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="99465-240">アルバムを一覧から削除されたことを示す、インデックスへのリダイレクト</span><span class="sxs-lookup"><span data-stu-id="99465-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="99465-241">これをテストするには、アプリケーションを実行し、/StoreManager を参照します。</span><span class="sxs-lookup"><span data-stu-id="99465-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="99465-242">一覧からアルバムを選択し、[削除] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="99465-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="99465-243">これには、削除の確認画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="99465-244">[削除] ボタンをクリックすると、アルバムを削除し、ストア マネージャーのインデックスのページでは、アルバムが削除されたことを示しています us 返します。</span><span class="sxs-lookup"><span data-stu-id="99465-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="99465-245">カスタム HTML ヘルパーを使用してテキストを切り捨てる</span><span class="sxs-lookup"><span data-stu-id="99465-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="99465-246">ストア マネージャーのインデックス ページとして潜在的な問題の 1 つをしました。</span><span class="sxs-lookup"><span data-stu-id="99465-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="99465-247">アルバム タイトル、アーティスト名プロパティは両方とも十分に長い書式が、テーブル スロー可能性があります。</span><span class="sxs-lookup"><span data-stu-id="99465-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="99465-248">これらおよびその他のプロパティで、ビューを簡単に切り捨てることができるようにするためのカスタム HTML ヘルパーを作成します。</span><span class="sxs-lookup"><span data-stu-id="99465-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="99465-249">Razor の@helper構文が行われたら、ビューで使用するための独自のヘルパー関数を作成する非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="99465-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="99465-250">/Views/StoreManager/Index.cshtml ビューを開き、次のコードを追加直接後に、@model行です。</span><span class="sxs-lookup"><span data-stu-id="99465-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="99465-251">このヘルパー メソッドは、文字列とを許可する最大長を使用します。</span><span class="sxs-lookup"><span data-stu-id="99465-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="99465-252">ヘルパーが出力として指定されたテキストが指定された長さより短い場合は、-はします。</span><span class="sxs-lookup"><span data-stu-id="99465-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="99465-253">長い場合は、テキストが切り捨てられ、残りの部分の「...」を表示します。</span><span class="sxs-lookup"><span data-stu-id="99465-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="99465-254">アルバム タイトル、アーティスト名の両方のプロパティが 25 文字未満であることを確認、切り捨てのヘルパーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="99465-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="99465-255">下の新しい切り捨てヘルパーを使用して完全なビュー コードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99465-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="99465-256">今すぐ/StoreManager/URL を参照して、アルバムとタイトルが、最大長以下保持されます。</span><span class="sxs-lookup"><span data-stu-id="99465-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="99465-257">注: を作成して、1 つのビューで、ヘルパーの使用の簡単な例を示します。</span><span class="sxs-lookup"><span data-stu-id="99465-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="99465-258">サイト全体で使用できるヘルパーの作成に関する詳細については、個人用ブログの投稿を参照してください: [http://bit.ly/mvc3-helper-options。](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="99465-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="99465-259">[前へ](mvc-music-store-part-4.md)
[次へ](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="99465-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>