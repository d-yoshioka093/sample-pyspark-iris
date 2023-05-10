# sample-pyspark-iris

## Overview

これは、`Kedro 0.18.7`を使用して生成された、新しいKedroプロジェクトです。
プロジェクトのアーキテクチャーとして、pysparkを使用してirisの予測タスクを実行します。

詳細情報、基本的なアーキテクチャーの情報については、[Kedroドキュメント](https://kedro.readthedocs.io)を参照してください。

## Rules and guidelines

テンプレートの効果を最大限に引き出すには：

* `.gitignore` ファイルから定義を削除しない
* [data engineering convention](https://kedro.readthedocs.io/en/stable/faq/faq.html#what-is-data-engineering-convention)に従い、結果が再現できることを確認
* データをリポジトリにコミットしない
* 認証情報やローカル設定をリポジトリにコミットせず、すべての認証情報とローカル設定を `conf/local/` に保存
* 改善が必要な場合、必ずレビューの上でリポジトリにブランチをマージすること

## How to install dependencies

仮想環境を作成し、当プロジェクト専用のpython実行環境を追加してください。

```
conda create --name kedro-environment python=3.10
```

`pip` をインストールする場合は `src/requirements.txt`で、~~ `conda` をインストールする場合は `src/environment.yml` で~~、依存関係を宣言してください。

`pip`インストール:

```
pip install -r src/requirements.txt
```

ローカル環境で`spark`を実行するため、`spark`と`hadoop`の実行環境をローカルPCに構築する必要があります。構築のイメージは所定のWebページより、それぞれに必要な実行ファイル群をローカルPCに配置し、環境変数を追加してそれらの実行ファイルがWindows上で認識される必要があります。
詳細については、[winutilsのREADME.md](https://github.com/kitfactory/winutils)を参照してください。2.2のVisualC++インストールは不要です。

ライブラリのバージョン:
　spark-3.4.0　hadoop-3.3.5

## How to run your Kedro pipeline

kedroプロジェクト実行:

```
kedro run
```

kedro run時のログ出力設定については、debugレベルまで出力するように定義しています。より簡易なログレベルに変更したい場合、`conf\base\logging.yml`の`#log level変更`部分を`INFO`に変更してください。

## How to test your Kedro project

テスト実行:  
※テストの書き方については、`src/tests/test_run.py` ファイルを参照

```
kedro test
```

coverage thresholdを設定するには、`.coveragerc` ファイルにアクセスします。

## Project dependencies

To generate or update the dependency requirements for your project:

```
kedro build-reqs
```

This will `pip-compile` the contents of `src/requirements.txt` into a new file `src/requirements.lock`. You can see the output of the resolution by opening `src/requirements.lock`.

After this, if you'd like to update your project requirements, please update `src/requirements.txt` and re-run `kedro build-reqs`.

[Further information about project dependencies](https://kedro.readthedocs.io/en/stable/kedro_project_setup/dependencies.html#project-specific-dependencies)

## How to work with Kedro and notebooks

> Note: Using `kedro jupyter` or `kedro ipython` to run your notebook provides these variables in scope: `catalog`, `context`, `pipelines` and `session`.
>
> Jupyter, JupyterLab, and IPython are already included in the project requirements by default, so once you have run `pip install -r src/requirements.txt` you will not need to take any extra steps before you use them.

### Jupyter
To use Jupyter notebooks in your Kedro project, you need to install Jupyter:

```
pip install jupyter
```

After installing Jupyter, you can start a local notebook server:

```
kedro jupyter notebook
```

### JupyterLab
To use JupyterLab, you need to install it:

```
pip install jupyterlab
```

You can also start JupyterLab:

```
kedro jupyter lab
```

### IPython
And if you want to run an IPython session:

```
kedro ipython
```

### How to convert notebook cells to nodes in a Kedro project
You can move notebook code over into a Kedro project structure using a mixture of [cell tagging](https://jupyter-notebook.readthedocs.io/en/stable/changelog.html#release-5-0-0) and Kedro CLI commands.

By adding the `node` tag to a cell and running the command below, the cell's source code will be copied over to a Python file within `src/<package_name>/nodes/`:

```
kedro jupyter convert <filepath_to_my_notebook>
```
> *Note:* The name of the Python file matches the name of the original notebook.

Alternatively, you may want to transform all your notebooks in one go. Run the following command to convert all notebook files found in the project root directory and under any of its sub-folders:

```
kedro jupyter convert --all
```

### How to ignore notebook output cells in `git`
To automatically strip out all output cell contents before committing to `git`, you can run `kedro activate-nbstripout`. This will add a hook in `.git/config` which will run `nbstripout` before anything is committed to `git`.

> *Note:* Your output cells will be retained locally.

## Package your Kedro project

[Further information about building project documentation and packaging your project](https://kedro.readthedocs.io/en/stable/tutorial/package_a_project.html)
