# AML-Handson
Azure Machine Learning Hands-on

# 必要なもの


- Microsoft Account
- Azure の Subscription

    お持ちない方は、Azure Free Trial へ。

    https://azure.microsoft.com/ja-jp/free/

# コンテンツ

- hello-aml.ipynb

    Azure Machine Learning の Python SDK を使った、学習部分について一通りの機能を試します。

      - Workspace への接続
      - 学習用 VM の設定
          コード上は `GPU` クラスターを作っています。無料トライアルでは、即座に使えませんので、`vm_size` に `STANDARD_D2_V2` などを指定して、`CPU` クラスターへ変更ください。
      - DataStore の設定
      - 学習用のスクリプトの実行 (PyTouch)
      - 学習結果の可視化
      - Azure Container Instance へデプロイ


# 参考ドキュメント

- Azure Notebooks:
 
    https://docs.microsoft.com/ja-jp/azure/notebooks/


- Azure Machine Learning:

    https://docs.microsoft.com/ja-jp/azure/machine-learning/service/
