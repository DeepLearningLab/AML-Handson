# AML-Handson
Azure Machine Learning Hands-on

# 必要なもの

- Microsoft Account
- Azure の Subscription

    お持ちない方は、Azure Free Trial へ。ただし、`GPU` インスタンスは *利用できません* ので、CPU のみでお願いします。

    https://azure.microsoft.com/ja-jp/free/

- Azure Notebook へのサインイン

    Azure Notebook の利用には Azureのアカウントがなくても行えます。Microsoft Account のみでOKです。

    ですが、このハンズオンでは *シングルサインオン* 出来るように、既存のAzure のアカウントで Azure Notebook にもログインできる、という前提で進めます。

    クイック スタート:サインインとユーザー ID の設定:

    https://docs.microsoft.com/ja-jp/azure/notebooks/quickstart-sign-in-azure-notebooks


# Azure Machine Learning services の作成と構成

## 1. Azure Machine Learning ワークスペースの作成

こちらのドキュメントを参考に、Azure Machine Learning ワークスペースを作成してください。

Azure Machine Learning Services ワークスペースを作成し、管理する:

https://docs.microsoft.com/ja-jp/azure/machine-learning/service/how-to-manage-workspace


## 2. Azure Notebook 上 へのハンズオンコンテンツのコピー (クローン)

Github にあるコンテンツをクローンします。

GitHub からプロジェクトをインポートする:

https://docs.microsoft.com/ja-jp/azure/notebooks/create-clone-jupyter-notebooks#import-a-project-from-github


インポート元

```
https://github.com/DeepLearningLab/AML-Handson
```


ノートブックで Azure Machine Learning service を使用する:

https://docs.microsoft.com/ja-jp/azure/notebooks/use-machine-learning-services-jupyter-notebooks

## 3. Azure Notebook のプロジェクトから、Azure Machine Learning services のワークスペース への接続

    接続文字列を作成します。

    以下の Notebook を開いて、実行してください。
    
## [00.configuration.ipynb](./00.configuration.ipynb)

    Azure Machine Learning services の 利用確認
    
      - SDK の動作確認
          Azure Notebook には Azure Machine Learning services の Python SDK がインストール済みです
      - Workspace への接続情報ファイルの作成 (config.json)
      - (option) AmlCompute の作成

Workspace のパラメーターは、Azure Portal にあります。

https://docs.microsoft.com/ja-jp/azure/machine-learning/service/how-to-configure-environment#workspace


# Azure Machine Learning services を使った深層学習の実行

## [01.train-deploy_pytorch.ipynb](./01.train-deploy_pytorch.ipynb)

    Azure Machine Learning の Python SDK を使った、学習部分について一通りの機能を試します。ここでは、PyTouch で学習を行います。 

      - Workspace への接続
      - 学習用 VM の設定
          コード上は `GPU` クラスターを作っています。無料トライアルでは、即座に使えませんので、`vm_size` に `STANDARD_D2_V2` などを指定して、`CPU` クラスターへ変更ください。
      - DataStore の設定
      - 学習用のスクリプトの実行 (PyTorch)
      - 学習結果の可視化
      - Azure Container Instance へデプロイ
      - REST での推論実行


## [02.train-hyperparametertune-deploy_chainer.ipynb](./02.train-hyperparametertune-deploy_chainer.ipynb)

    Chainer を使っての、学習部分と、Hyperparamter Tuning について一通りの機能を試します。

      - Workspace への接続
      - 学習用 VM の設定
      - DataStore の設定
      - 学習用のスクリプトの実行 (Chainer)
      - 学習結果の可視化
      - Hyperparamter Turning の設定
      - 学習用のスクリプトの実行 (Chainer)
      - Azure Container Instance へデプロイ
      - REST での推論実行


## 他の Framework のサンプル

TensorFlow などのサンプルコードはこちらになります。

https://github.com/Azure/MachineLearningNotebooks/tree/master/how-to-use-azureml/training-with-deep-learning


# GPU が使えない方のために

CPU でも学習時間は比較的短い 有名なデータセットである MNIST を使ったものを試します。

Source:

https://github.com/Azure/MachineLearningNotebooks

## [11.automated-machine-learning_classification_auto-ml-classification.ipynb](11.automated-machine-learning_classification_auto-ml-classification.ipynb)

    Automated Machine Learning の機能を試します。MNISTがデータセットです。


## [12.automated-machine-learning_classification-with-deployment_auto-ml-classification-with-deployment.ipynb](12.automated-machine-learning_classification-with-deployment_auto-ml-classification-with-deployment.ipynb)

  Automated Machine Learning に加えて、Azure Container Instance へデプロイまで行います。


# うまくいかなかったとき

- Azure Notebook で Azure Machine Learning services の SDK が動作しない

  - 現在の Azure Machine Learning services の SDKは、 Python 3.6 で動作します。Azure NotebookのKernel で Pythonのバージョンを確認してください。

- Azure Machine Learning services の Workspace 接続用のconfig.jsonファイル作成がうまくうごかない

    - config.json を手動で作成ください。

        参照: ワークスペース構成ファイルを作成する

        https://docs.microsoft.com/ja-jp/azure/machine-learning/service/how-to-configure-environment#workspace

- GPU クラスターの作成に失敗する

    無料アカウントの場合、GPU インスタンスのクォータ (利用可能CPU数) が不足しています。0 になっています。もし GPU インスタンスを利用したいという場合は、従量課金のアカウントへ切り替えてください。

    有償のアカウントの場合、GPUのコア数が不足している場合があります。サポートチケットを作成して、GPUコア数の引き上げのリクエストをしてください。即座に実施できるわけではなく、数営業日かかる場合もあります。

    Resource Manager の vCPU クォータを増やす要求

    https://docs.microsoft.com/ja-jp/azure/azure-supportability/resource-manager-core-quotas-request

    Azure リソースのクォータの管理と要求

    https://docs.microsoft.com/ja-jp/azure/machine-learning/service/how-to-manage-quotas
 

- AmlCompute や、Data Science VM など、作成したはずなのに利用ができない

    `コンピューティング` として Azure Machine Learning Workspace内で設定がされているのに、CPUクォータ不足などがあって「失敗」という状況のまま、残っている場合があります。
    
    Azure Portal の、Azure Machine Learning services Workspace の `コンピューティング` から、削除ください。

    - AmlCompute -> 削除
    - Data Science VM -> でタッチ


- Azure Machine Learning services 既知の問題

https://docs.microsoft.com/ja-jp/azure/machine-learning/service/resource-known-issues

# 参考ドキュメント

- Azure Notebooks:
 
    https://docs.microsoft.com/ja-jp/azure/notebooks/

- Azure Machine Learning:

    https://docs.microsoft.com/ja-jp/azure/machine-learning/service/
