## 章立て
APIリソースとkubectl

## memo
* リソースの作成にもkubectl applyを使うべき（差分更新を上手にやるため）
* マニフェストファイルの中に複数のリソースを書く場合 `---` が区切りになり、上から順に実行される
* 複数のマニフェストファイルを同時に適応するにはディレクトリを指定するとファイル名順に適応される
* アノテーションは `システムコンポーネントのためにデータを保存` したり、 `全ての環境では利用できない設定を行う` ために使われるらしい
* ラベルはリソースを分割するために使われる（グルーピングなど）。最初にいくつか決めてから使うようにしましょう（プロジェクト、アプリケーションの種類、アプリケーションのバージョン、環境など）
* apply時に `--prune` オプションをつけると、マニフェストから削除されたリソースを自動的に削除してくれるもの
  * 基本的にはラベルを指定して使いませう
  * 実行したディレクトリ違いなどで誤って消えてしまう事故も考えられるのでディレクトリ構成とラベルの設計には注意が必要
* editでエディター上で編集可能（EDITOR or KUBE_EDITORで指定されているもの）
* `kubectl get all` で全てのリソースが見れちゃうおー
* `kubectl describe`で`node` を指定すると起動しているPodのリソース使用率やPodに確保したリソースもみれる
* `kubectl top` でPod内のコンテナが使用しているりそーすの使用量がみれる(nodeとpodなど指定してみると良い)、 `--containers` でコンテナごとの指定も可能
* `exec` や `logs` に関してはdockerコマンドとほぼ同じ
  * logの確認は`stern`というものを使うと便利みたい
  * `--timestamps` , `--selector(特定のラベルのみなど)`などが指定可能
* `-v` オプションでログレベルを指定でき、`-v=6`以降でk8s masterとの通信内容がみれる模様
* `kube-ps1` というのが現在触っているクラスタとnamespaceを表示してくるの便利
