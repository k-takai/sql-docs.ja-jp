---
title: "どのような &#39; Machine Learning のサービスの |Microsoft ドキュメント"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8719ec8be1c0f7b7b0dc72093707829c30ebbb3f
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>SQL Server の Machine Learning のサービスの新機能

SQL Server 2016 では、Microsoft には、SQL Server R Services、SQL Server データベース エンジンと、R 言語を統合することにより、エンタープライズ規模のデータ サイエンスをサポートする機能が導入されました。

SQL Server 2017、機械学習は一般的な Python 言語のサポートを追加するより強力なになります。 新しい名前は、新しい言語のサポートと共に: **Machine Learning Services (In-database)**です。

最新のお知らせは、ここをキャッチします。 [SQL Server 2017 の Python: データベース内の機械学習の強化](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017-release-candidate-2"></a>SQL Server 2017 Release Candidate 2 の新機能

Microsoft Machine Learning サーバー SQL Server では、今すぐを構築およびマシン ラーニング ソリューションを配置するための包括的なサポートを提供します。 このリリースの要点を次に示します。

> [!IMPORTANT]
> 
> R、Python の使用を含む、マシン学習サービスは現在サポートされていません、Linux 上または Azure SQL データベース、SQL Server を実行している場合。 今後のリリースで変更を探します。
> 
> ただし、予測関数を使用してネイティブ スコアリングは現在サポートされて Linux のエディションでします。 
 
### <a name="in-database-python-integration"></a>データベース内の Python の統合

Python ストアド プロシージャ、またはを実行する計算コンテキストとして、SQL Server コンピューターを使用してリモートで Python を実行します。 この統合表示の Python の開発者とデータ科学者、SQL Server の power を使用して、Microsoft からなどの技術革新を探索する膨大なコミュニティのための新しい手法**revoscalepy**と**microsoftml**.

SQL Server の開発者にアクセスする広範な Python ライブラリ scikit などの一般的なフレームワークを含む、オープン ソース エコシステムから-Tensorflow、Caffe および Theano/Keras を説明します。 

データベースでは、機械学習; の単に Python を実行しているが、多数の他の潜在的なアプリケーションとの統合に Python SQL より高度な強力なソリューションを提供するそれぞれの言語の長所を活用することがあります。

+ **revoscalepy**

    このリリースでは最終バージョンの**revoscalepy**、ストリーミング RevoScaleR のアルゴリズムのスケーラブルな対応する Pythonic を渡しています。 線形とロジスティック回帰、デシジョン ツリー、ブースト ツリー、およびランダム フォレスト、すべて並列処理、およびリモート計算コンテキストで実行中の対応の Python モデルを作成することができます。

    詳細については、次を参照してください。 [revoscalepy は](python/what-is-revoscalepy.md)します。

+ Python のリモート計算コンテキスト

    このリリースでは、複数のデータ ソースとリモート計算コンテキストの使用をサポートします。 データ科学者や開発者は、データを参照するか、データを移動せずにモデルを構築する、リモートの SQL Server での Python コードを実行できます。 リモート計算コンテキストを使用する必要**revoscalepy**です。

+ Microsoft Machine Learning Server (スタンドアロン) での Python のサポート

    SQL Server 2017 には、Python と R プラットフォームのスタンドアロン バージョンをインストールするオプションが含まれています。 Machine Learning のサーバーを使用するは、配布し、SQL Server を使用せずに R または Python コードをスケールします。

    Microsoft Machine Learning のサーバーでの Python の使用の例は、次を参照してください。[発行 Python コードを使用すると](python/publish-consume-python-code.md)です。

### <a name="new-algorithms"></a>新しいアルゴリズム

**MicrosoftML** R、Python の両方のパッケージには、最先端の機械学習アルゴリズムが含まれています、リモートのスケールまたはで実行できるデータの変換は、コンテキストを計算します。 深層ニューラル ネットワークのカスタマイズ可能な高速なデシジョン ツリーとデシジョン フォレスト、線形回帰、およびロジスティック回帰アルゴリズムが含まれます。

MicrosoftML パッケージは、R、Python の両方のインターフェイスが付属してされ、Microsoft Machine Learning Server バージョン 9.2.0 に基づいています。

詳細については、次を参照してください。 [MicrosoftML 概要](using-the-microsoftml-package.md)と[for Python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)です。

### <a name="operationalization"></a>操作運用

このリリースには、展開および機械学習タスクを配布するために、複数のオプションと機能が含まれています。

+ T-SQL の使用

    呼び出すことができる Python コードを使用して、T-SQL での Python の統合を意味`sp_execute_external_script`です。 このセキュリティで保護されたインフラストラクチャでは、Python モデルと単純なストアド プロシージャを使用して、アプリケーションから呼び出すことができるスクリプトのエンタープライズ レベルの展開できるようにします。 その他のパフォーマンスは、SQL から Python プロセスと MPI リングの並列化にデータをストリーミングでです。

+ **mrsdeploy** for Python

    **Mrsdeploy** Microsoft R Server ようになりました、web サービスとしての Python モデルとスクリプトの展開をサポートされ、マシン学習 Server (スタンドアロン) のオプションとして利用可能なパッケージ化します。 そのしくみの例は、次を参照してください。[発行 Python コードを使用すると](python/publish-consume-python-code.md)です。

+ パフォーマンス

    Microsoft はスコアリングのためのパフォーマンスの境界をプッシュされます。 ごとに 100万行を処理したデータベース内のスコアリングと 2 番目の R モデルを使用します。 このリリースでは、新機能で**リアルタイム スコアリング**と**ネイティブ スコアリング**単一行のスコアと小規模でパフォーマンスの向上をバッチ処理もサポートします。 

### <a name="realtime-scoring-and-native-scoring"></a>リアルタイムのスコアリングと、ネイティブのスコアリング

リアルタイムのスコアリングは、最適化されたバイナリ形式で格納されているモデルを読み込むし、R ランタイムを呼び出さずに予測を生成するネイティブの C++ ライブラリに依存します。 これにより、スコア付けの操作をはるかに高速です。

さらに、SQL Server 2017 の今回のリリースに含まれるネイティブ T-SQL 関数高速スコアリングのため Linux 上であっても、SQL Server の任意のエディションで実行することができます。 関数には、R または追加の構成のインストールは不要です。 つまり、他の場所で、モデルのトレーニング、SQL Server に保存および R. を呼び出さないでスコアリングを実行し、この機能と呼ばれます_ネイティブ スコアリング_です。

  - ネイティブ スコアリングは、SQL Server 2017 でのみ使用できます。 Linux を含む、SQL Server の任意のエディションで実行できる T-SQL 関数を使用します。
 - リアルタイムのスコア付けすると、SQL Server の 2017 でおよび Microsoft Machine Learning のサーバーでがサポートされます。 実行することができますストアド プロシージャまたはリアルタイムの R コードのスコア付けを実行します。
 - リアルタイムのスコアも利用できます for SQL Server 2016 インスタンスは Microsoft R Server の最新のリリースにアップグレードした場合。

詳細については、次の記事を参照してください。

 + [リアルタイムのスコアリング](real-time-scoring.md)
 + [ネイティブのスコアリング](sql-native-scoring.md)
 + [リアルタイムのスコアリングまたはネイティブ スコアリングを実行する方法](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-ml-experience-and-get-pre-trained-models"></a>ML エクスペリエンスをアップグレードし、事前トレーニング済みモデルの取得

SQL Server 2016 の R Services の以前のバージョンをインストールした場合重要度の最新のライフ サイクル ポリシーを使用するようにサーバーを切り替えることによって、最新バージョンにアップグレードすることができますようになりました。 これにより、R の高速のリリース サイクルの活用し、すべての R コンポーネントを自動的にアップグレードできます。 詳細については、 [Microsoft R Server 9.0.1](https://docs.microsoft.com/r-server/whats-new-in-r-server)に関する記事を参照してください。

インストーラーでは、バイナリ形式で事前トレーニング済みモデルのコレクションをインストールするオプションも提供します。 これらのモデルでは、ここで難しい可能性があるモデルをトレーニングする大規模なデータセットを検索する顧客の画像認識などのシナリオで機械学習をサポートします。 事前トレーニング済みモデルの 1 つをインストールした後は、時間とコストがこのような大規模で複雑なモデルのトレーニングに関係することがなく、独自のデータの予測使用することができます。

詳細については、次を参照してください[事前トレーニング済みモデルを SQL Server のインストール。](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>パッケージの管理

このリリースには、SQL server パッケージ管理の多くの機能強化が含まれています。 たとえば、次のオブジェクトにアクセスできます。

- DBA は、管理およびアクセス許可を監査するデータベース ロール
- T-SQL で EXTERAL ライブラリの作成ステートメント
- インストールするための R 関数の豊富なセットは、削除、または、ユーザーが所有するパッケージを一覧表示します。

詳細については、次を参照してください。[パッケージの管理](r/r-package-management-for-sql-server-r-services.md)です。

### <a name="get-started"></a>作業を開始します。

+ [SQL Server の Machine Learning のサービスでの Python の設定します。](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [SQL Server の Machine Learning のサービスで R を設定します。](r/set-up-sql-server-r-services-in-database.md)

+ [Machine learning のチュートリアル](tutorials/machine-learning-services-tutorials.md)