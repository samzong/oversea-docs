# Poetry

poetry 是目前比较流行的 Python 环境管理工具 和 包管理工具，对多项目开发时的环境隔离有非常大的帮助，同时集成了包管理能力。

> 官方网站  [https://python-poetry.org/](https://python-poetry.org/)   集成了所有 Poetry 最新的使用文档，以下仅在我的环境上经过验证


### 安装方式

```python
# In Pip
- 安装 pip install poetry # pip3
- 更新 poetry self update

# In my Mac
- 安装 brew install poetry
- 更新 brew upgrade poetry

# In my CentOS
- 安装 curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
- 更新 poetry self update
```

### 配置技巧相关

在开始使用前，建议先对poetry 的配置有些了解，并调整为适合你的方式，主要是调整一下虚拟环境的安装位置

> `poetry config` poetry 相关的查看和编辑的命令

```python
~ poetry config --list  # 获取当前 poetry 的配置情况

cache-dir = "/Users/$username/Library/Caches/pypoetry"
experimental.new-installer = true
installer.parallel = true
virtualenvs.create = true
virtualenvs.in-project = true
virtualenvs.path = "{cache-dir}/virtualenvs"  # /Users/$username/Library/Caches/pypoetry/virtualenvs

```

| **配置项目** | **配置内容** | **配置项说明** | **建议配置** |
| --- | --- | --- | --- |
| cache-dir | String | 缓存目录配置，使用 poetry 安装的包源文件都会缓存到这个目录。 | 不建议更改 |
| installer.parallel | boolean | 此配置会被忽略 |  |
| virtualenvs.create | boolean | 默认为true，如果当前工程的虚拟环境不存在，就创建一个 | 不建议更改 |
| virtualenvs.in-project | boolean | None：poetry 会在系统特定目录创建一个.venv目录，由下面的 path 参数指定,true： poetry 会在项目根目录创建一个.venv目录; false： poetry 将会忽略已存在的.venv目录 | **《建议修改》** 推荐这种方式，在项目根目录创建虚拟环境，这样就算移动目录位置也不影响虚拟环境的使用 |
| virtualenvs.path | string | 默认是{cache-dir}/virtualenvs，虚拟环境创建的目录，如果上面的 in-project 为 true，此配置就无效 | 不建议更改 |


> 建议 在使用前 启用 virtualenvs.in-project ，这样会在每个项目下有一个.venv 方便隔离管理

```python
# poetry 配置说明
poetry config virtualenvs.in-project true
```


### poetry 常用指令说明

| **Poetry Command** | **解释** |
| --- | --- |
| $ poetry --version | 显示您的 Poetry 安装版本。 |
| $ poetry new | 创建一个新的Poetry项目。 |
| $ poetry init | 将 Poetry 添加到现有项目中。 |
| $ poetry run | 使用 Poetry 执行给定的命令。 |
| $ poetry add | 添加一个包pyproject.toml并安装它。 |
| $ poetry update | 更新项目的依赖项。 |
| $ poetry install | 安装依赖项。 |
| $ poetry show | 列出已安装的软件包。 |
| $ poetry lock | 将最新版本的依赖项固定到poetry.lock. |
| $ poetry lock --no-update | 刷新poetry.lock文件而不更新任何依赖版本。 |
| $ poetry check | 验证pyproject.toml。 |
| $ poetry config --list | 显示 Poetry 配置。 |
| $ poetry env list | 列出项目的虚拟环境。 |
| $ poetry export | 导出poetry.lock为其他格式。 |


### 新项目初始化流程


> 这里以 初始化一个  FastAPI 项目作为 实例

```bash
➜  fastapi poetry new fastapi-demo
Created package fastapi_demo in fastapi-demo
➜  fastapi ls -lh fastapi-demo
total 8
-rw-r--r--  1 samzonglu  staff     0B  2 15 14:28 README.rst
drwxr-xr-x  3 samzonglu  staff    96B  2 15 14:28 fastapi_demo
-rw-r--r--  1 samzonglu  staff   304B  2 15 14:28 pyproject.toml
drwxr-xr-x  4 samzonglu  staff   128B  2 15 14:28 tests

➜  fastapi cd fastapi-demo
➜  fastapi-demo poetry env use 3.10.2  # 配置项目的虚拟环境

```


### requirements.txt 已存在项目使用poetry


这里会遇到一个问题，已存在的项目基本都已经有了 requirements.txt， 所以 poetry 最好可以直接读取它

```shell
poetry add `cat requirements.txt`
```

将项目依赖导出为  requirements.txt

```shell
poetry export --output requirements.txt
```
