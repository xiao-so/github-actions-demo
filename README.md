# github-actions-demo
本项目用于熟悉和练习 GitHub Actions
使用 GitHub Actions,需要在公共仓库操作
## quick-start
1. 创建 `.github/workflows` 目录
2. 在目录下创建一个 `github-actions-demo.yml` 文件
3. 修改文件内容
```yaml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```
4. 提交文件，推送到远程分支 quick-start

可以在项目 Actions 里找到如下标题的信息，其中 `xiao-so` 为 `${{ github.actor }}`

> xiao-so is testing out GitHub Actions 🚀

点击可以查看详细执行结果



