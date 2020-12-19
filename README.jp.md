# Reactive Rails ガイド

このリポジトリは、概念を簡単に紹介し、Reactive Railsの旅に役立つ可能性のある役立つコンテンツを紹介することを目的としています。このリポジトリをウォッチして、Reactive RailsについてWebで公開されている最新情報を入手してください。（コントリビュートは大歓迎です。PRを送ってください。）

## Reactive Railsとは何ですか？

_Reactive Rails_ は、Ruby on Railsを使用したWebアプリケーション開発のある設計哲学またはアーキテクチャスタイルを説明するための用語です。このスタイルは、RESTful（aka「vanila」）HTMLサーバーでレンダリングされたアプリケーションと、Rails API + React または他のフロントエンドフレームワークのシングルページアプリケーション（SPA）の真ん中に位置するものです。

Reactive Railsは、フルスタックRails開発者の小さなチームが、サーバーでレンダリングされたHTMLと最小限のJavaScriptを使用して、リッチでリアルタイムのユーザーエクスペリエンスを実現できるようにします。これは、Elixirで書かれたRailsの競合Webフレームワークである[Phoenix LiveView](https://github.com/phoenixframework/phoenix_live_view)に（恥じることなく）触発され、小さなチームが大きなことを行えるようにするというRuby on Railsフレームワークのモチベーションとなった精神を尊重しています。  

### なぜ「Reactive（リアクティブ）」と呼ばれるのですか？

Reactive Railsは、ユーザーのイベントに対する高速な非同期処理（fast asynchronous _reaction_）を可能にします。これは、最近までReactやAngularなどのフロントエンドフレームワークを使用した場合にのみ可能でした。通常のサーバーでレンダリングされたページリクエストの処理には、少なくとも100〜500ミリ秒かかります。サーバーから送信されたHTMLペイロードを使用してブラウザが画面を再レンダリングするために必要な時間を考慮すると、リクエストサイクルは次のようになります。多くの場合、ミリ秒単位で測定されます。

Reactive Railsアプリでは、ユーザーの操作は通常のHTTPリクエストではなくWebSocketを介してサーバーに渡されます。軽量なハンドラーはサーバー上のアプリケーションの状態を変更し、現在のページが自動的に再レン​​ダリングされてブラウザーに送り返されます。 DOMの差分は、ドキュメント全体を再レンダリングすることなく、新しいアプリケーションの状態を反映するように画面を変更するために使用されます。ベストケースなシナリオの場合、画面は20〜30ミリ秒で更新できます。 200〜300ミリ秒未満のページの更新は、通常、感知できないと見なされています。

このスタイルが「Reactive」と呼ばれるもう1つの理由は、多くの人が行っているように、テンプレートだけでなくコンポーネント指向のビューを追加すると、デザインパターンがReactでアプリを作成するために使用されるものにだんだん似てくることです。主要なプログラミング言語は、JavaScriptではなくRubyのままです。

### Reactive Rails 技術スタック

Reactive Railsは、[ActionCable](https://railsguides.jp/action_cable_overview.html)によって可能になります。[Turbolinks 5](https://github.com/turbolinks/turbolinks)と[StimulusJS](https://stimulusjs.org/)からも影響を受けていますが、この2つは必ずしも使用する必要はありません。

Reactive Railsの開発を行うために使用できるフレームワークは他にもありますが、最も牽引力と、勢い、コミュニティを備えているのは、[Nate Hopkins aka hopsoft](https://github.com/hopsoft) によって作成された StimulusReflex です。 これは StimulusJS の基盤の上に大きく構築されています。

#### StimulusReflex

[StimulusReflex](https://docs.stimulusreflex.com/)は、Railsを「Reactive」にするために追加されたメインライブラリです。これはStimulusJSに大きく影響を受けており、ブラウザーイベントにフックするための書き方は同じですが、ローカルのJavaScriptベースのコントローラーでアクションをトリガーする代わりに、ActionCableチャネルを介してサーバーでアクションをトリガーします。イベントはサーバー側で受け取りますが、これは "reflex" として実装されています。"reflex" は、主にサーバーの状態の変更に関する軽量なコントローラーのアクションです。

#### CableReady

StimulusReflexは、[CableReady](https://cableready.stimulusreflex.com/)の上に構築されています。これは、主にサーバーからブラウザーのDOMを直接制御できるようにすることで、その機能を大幅に強化するActionCableのラッパーです。

#### ViewComponent

[ViewComponent](https://github.com/github/view_component)は、Githubのメインのモノリスアプリケーションから抽出されたフレームワークであり、「再利用可能、テスト可能、カプセル化」されたビューコンポーネントを構築するために使用されます。ビューコンポーネントを使用すると、Reactive Railsの開発は、ビューを構築するためのコンポーネントクラスに重点が置かれているため、Reactのコードを書いているように感じられます。

#### ViewComponentReflex

[ViewComponentReflex](https://github.com/joshleblanc/view_component_reflex)を使用すると、ビューコンポーネントコードに reflex を直接書くことができるため、[Motion](https://github.com/unabridged/motion)と非常に近い感覚です。

## 例とデモ/サンプルコード

[StimulusReflex showcase](http://expo.stimulusreflex.com/)チャット、カレンダー、Todoなど、完全なソースコード付き。

[ViewComponentReflex showcase](https://view-component-reflex-expo.grep.sh/) には、Local State、ローダー、Todo、およびデータテーブルの例とコードがあります。

[Shoelace](https://shoelace.style/)を使った[Toast-style alerts system](https://gist.github.com/obie/5c56d87c7b7e4e343ef7504349a69515)

[Modern Datatables](https://github.com/guillaumebriday/modern-datatables)は、2つのアプリと動いているデモを備えたリポジトリです。1つはサーバーレンダリングビュー、Stimulus、Stimulus Reflex、Turbolinksを備えた古典的で学校で学ぶようなRailsアプリケーションを備えています。もう1つは、バックエンドAPIとしてRailsを使用し、フロントエンドで完全な静的SPAとしてVue.jsを使用します。

[Boxdrop](https://github.com/marcoroth/boxdrop)は、StimulusReflexを使用して構築されたDropboxクローンであり、StimulusReflexを使用してアプリケーションを構築する方法を示しています。

## ビデオ

### The "Twitter in 10 minutes" video

今日のReactive Railsの（Rails開発者の間での）メインストリームは、Hopsoftの [Build a real-time Twitter clone in 10 mins with Rails and StimulusReflex](https://dev.to/codefund/build-a-real-time-twitter-clone-10-mins-with-rails-and-stimulusreflex-5h5c) から影響を受けています（ha！） このビデオは、Ruby on Railsが世界をワクワクさせる発端となった、DHHの[How to build a blog engine in 15 minutes](https://www.youtube.com/watch?v=Gzj723LkRJY&feature=youtu.be)と同じようなものです。

[Mike McCracken](https://medium.com/@mikemccracken/stimulusreflex-twitter-clone-in-more-than-9-minutes-b556dc512a62)によるTwitterクローンチュートリアル付きの素晴らしいブログ投稿もあります。 

### チュートリアル

TechmakerTVによるRuby on Rails 6とStimulus Reflexを使用したリアクティブTodoリストの作成 [link](https://www.youtube.com/watch?v=eK1CM0MBF64)

Episode #209 - Reactive Applications with Stimulus Reflex by DriftingRuby [link to preview](https://www.youtube.com/watch?v=K9QeC9CsYiU)

Introduction to StimulusReflex by GoRails [link](https://www.youtube.com/watch?v=gbMbGOigjA8)

Create Fast Apps With Stimulus Reflex And RailsBytes Templates In Ruby On Rails 6 by Deanin [link](https://www.youtube.com/watch?v=hxqkTy2SB78)

Stimulus Reflex Morph Modes | Selector Morphs with Rails View Components by TechmakerTV [link](https://www.youtube.com/watch?v=bwFrjIC8wfE)

[Two Patterns for Stimulus Reflex form submissions](https://blog.minthesize.com/two-patterns-for-stimulus-reflex-form-submissions)

## 読みもの

ブログポストなど。

### ドキュメント

[StimulusReflex Documentation](https://docs.stimulusreflex.com/)

### イントロダクション的なブログ

[A future for Rails: StimulusReflex](https://headway.io/blog/a-future-for-rails-stimulusreflex)には、チャットアプリのソースが含まれています

[Reactive Rails Applications with StimulusReflex](https://dev.to/finiam/reactive-rails-applications-with-stimulusreflex-48kn)

### チュートリアル

[Twitter Clone with StimulusReflex gone Hybrid Native App](https://dev.to/julianrubisch/twitter-clone-with-stimulusreflex-gone-hybrid-native-app-17fm) は、HopsoftによるTwitterクローンのビデオを元に、ネイティブアプリを作ります。

[Reactive Map with Rails, Stimulus Reflex and Mapbox](https://dev.to/ilrock__/reactive-map-with-rails-stimulus-reflex-and-mapbox-1po4) は、Reactive Railsを活用してマップアプリケーションをすばやく構築します。

[Infinite Horizontal Slider with CableReady and the Intersection Observer API](https://dev.to/julianrubisch/infinite-horizontal-slider-with-cableready-and-the-intersection-observer-api-4o4i)

[Lightning fast reactive action with Stimulus Reflex partial morphs](https://dev.to/rolandstuder/lightning-fast-reactive-action-with-stimulus-reflex-partial-morphs-2fg5) introduces morphing in reflexes.

[Using Tippy.js with StimulusReflex and CableReady](https://dev.to/mepatterson/using-tippy-js-with-stimulusreflex-and-cableready-3gno)

### Hype

この[ワクワクするようなブログ記事](https://medium.com/@obie/react-is-dead-long-live-reactive-rails-long-live-stimulusreflex-and-viewcomponent-cd061e2b0fe2)は、私がReactive Railsが全てだと、そう思った時に書いたものです。

[Announcement of morph in StimulusReflex 3.3](https://dev.to/leastbad/stimulusreflex-v3-3-morphs-has-been-released-o3e)は、StimulusReflexコミュニティで、最も率直な意見を持つメンバーの1人であるleastbadによるものです。

## 便利なライブラリ

[Shoelace](https://shoelace.style/) コンポーネントについて考えたら、事前にパッケージ化されたWebコンポーネントを使用する方がはるかに魅力的ですから。

[Optimism](https://github.com/leastbad/optimism) drop-in remote form validation.

[Futurism](https://github.com/julianrubisch/futurism) lazy-load view partials.

[Turbolinks iOS Wrapper](https://github.com/turbolinks/turbolinks-ios/)は、React Nativeに対するReactive Railsとしてのアンサーになっています。

[StimulusComponents](https://github.com/stimulus-components)は、便利なStimulusコンポーネントのコレクションです。

[StimulusUse by Adrien Poly](https://github.com/stimulus-use/stimulus-use)は、Stimulusコントローラーのための、コンポーザブルな使用方法のコレクションです。

[StimulusControllers by Hopsoft](https://github.com/hopsoft/stimulus_controllers/tree/master/controllers/src) は、オートサジェストやクリップボードコピーなどの、便利なStimulusコントローラーのコレクションを備えています。

[Stimulus Form Utilities by Hopsoft](https://github.com/eelcoj/stimulus-form-utilities)は、任意の入力フィールドの文字数のカウントや自動テキストフィールドのサイズ変更などの便利なフォームヘルパーのコレクションです。

[StimulusReflexGlobalId](https://github.com/joshleblanc/stimulus_reflex_globalid)は、"reflex"の時にグローバルIDをインスタンス変数に自動的にマップします。

[StimulusShortcut](https://github.com/leastbad/stimulus-shortcut)は、キーストロークを要素のアクションに簡単にバインドします。

[TailwindCSS StimulusComponents](https://github.com/excid3/tailwindcss-stimulus-components)は、Bootstrapのコンポーネントに影響を受けています。

## テストリソース

[StimulusReflex Testing](https://github.com/podia/stimulus_reflex_testing)は、「reflex」のユニットテストをサポートしています。

## コミュニティ

[StimulusJSのコミュニティサイト](https://discourse.stimulusjs.org/)

## 関連プロジェクト

[Motion](https://github.com/unabridged/motion)は、StimulusReflexに最も近く、直接的な代替になるかもしれません。ピュアなRubyを使用したRailsアプリケーションの中に、リアクティブでリアルタイムなフロントエンドUIコンポーネントのための統合されたフレームワークを持ちます。

[Matestack](https://www.matestack.io/)も別の選択肢になりえます。

[Hyperstack](https://hyperstack.org/)は、Ruby DSLであり、Opalによってコンパイルされ、Webpackによってバンドルされ、Reactによって提供されます。

[Snabberb](https://github.com/tobymao/snabberb) Ruby / Opalで記述され、Snabbdomに基づく最小限のリアクティブフロントエンドWebフレームワークです。

[Sockpuppet](https://github.com/jonathan-s/django-sockpuppet) PythonでDjangoを使用して最新のリアクティブなリアルタイムアプリを構築します。

[Reactive Laravel](https://github.com/livewire/livewire)

[Reactive Phoenix](https://github.com/phoenixframework/phoenix_live_view) はElixirで書かれており、「Reactive Rails」のすべてに影響を与えました。

[Reactive ASP.NET](https://github.com/dotnet/aspnetcore/blob/master/src/Components/README.md)

[Prism](https://github.com/prism-rb/prism)は、RubyとWebAssemblyを使用してWebアプリケーションを作成するためのフレームワークです。

## Credit

_Hat tip to [Skatkov](https://github.com/skatkov/awesome-stimulusjs) for the idea._
