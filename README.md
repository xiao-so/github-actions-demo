# github-actions-demo
本项目用于熟悉和练习 GitHub Actions
使用 GitHub Actions,需要在公共仓库操作
## quick-start-ci
该分支用于练习持续集成（CI）的基本使用

### 自动打包 maven 并推送到 github release
`github-maven.yml`

```yaml
name: GitHub Actions CI Demo
run-name: package maven project
on:
  push:
    branches:
      - quick-start-ci
jobs:
  Package-Maven-Project:
    env:
      RELEASE_VERSION: "0.0.1"
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository code
        uses: actions/checkout@v3
      - name: Set up JDK 1.8
        uses: actions/setup-java@v2
        with:
          java-version: '8'
          cache: 'maven'
          distribution: 'temurin'
      # 使用 maven package
      - name: Build with Maven
        run: mvn clean package -e -U -B --file Hello-Maven/pom.xml
      # 移动打包好的 jar 文件到 staging 文件夹
      - run: mkdir staging && cp Hello-Maven/target/*.jar staging
      # 上传文件并发布到 Release
      - name: "Upload to release"
        uses: "marvinpinto/action-automatic-releases@latest"
        with:
          repo_token: "${{ secrets.GITHUB_TOKEN }}"
          automatic_release_tag: "${{ env.RELEASE_VERSION }}"
          prerelease: true
          title: "Release  ${{ env.RELEASE_VERSION }}"
          files: |
            staging/*.jar
```


