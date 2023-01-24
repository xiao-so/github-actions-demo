## 了解 GitHub  Actions 文件
> 分支：demo-action
>
> [demo-action](https://github.com/xiao-so/github-actions-demo/tree/demo-action)

GitHub  Actions 文件采用 YAML 语法，文件存放在代码仓库 `.github/workflows/` 文件夹下，可以有任意多个。

```{3}
├─.github
│  └─workflows
│          docs.yml
```

一份简单的文件示例如下，其中 demo-job 的 job 做了三件事：

1. checkout 当前仓库最新的代码
2. 列出仓库的文件
3. 执行 `echo 'finish'`命令，输出 finish 文本

```yaml
# 工作流的名称
name: demo-action

# 工作流运行的名称
run-name: ${{ github.actor }} run the demo-job 

# 工作流触发时机
on:
  # 每当 push 到 demo-job 分支时触发部署
  push:
    branches: [demo-job]
  # 手动触发部署
  workflow_dispatch:

# 定义 jobs
jobs:
  # 定义名为 demo-job 的 job
  demo-job:
    # 运行器使用的环境，此处为 ubuntu
    runs-on: ubuntu-latest
    # 定义执行的 steps 
    steps:
      # 这个 step 为 checkout 当前仓库的代码, name 为 step 名，可选
      # 使用(uses) https://github.com/actions/checkout 下打了 v3 tag的 action
      - name: Check out repository code
        uses: actions/checkout@v3
        # with 后面输入 action 需要的参数，这里表示最新的代码
        with:
          fetch-depth: 0
      - name: List files in the repository
        run: ls ${{ github.workspace }}
      # 输出 finish
      - run: echo "finish"
```

