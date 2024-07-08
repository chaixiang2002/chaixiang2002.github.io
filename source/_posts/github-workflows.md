```sh

gittagv1.0.1

gitpushorigin--tags

```

### 例子

具体操作如下：

1. 删除本地标签：

```sh

gittag-l | xargsgittag-d

```

2. 删除远程标签：

```sh

gitfetch--tags

gittag-l | xargs-I{}gitpushorigin:refs/tags/{}

```

3. 验证：

```sh

gittag-l

gitls-remote--tagsorigin

```

通过以上步骤，你可以清除本地和远程仓库中的所有标签。

### 注意

-`git tag -l` 列出所有标签。

-`xargs git tag -d` 删除本地所有标签。

-`git push origin :refs/tags/{}` 删除远程标签。

确保你已经同步了所有需要保留的标签信息，因为这些操作会彻底清除标签。





```ini
name: Package and release
# learn from https://github.com/tickbh/wmproxy/blob/main/.github/workflows/ci.yml
on:
  push:
    tags:
      - "v*"

permissions:
  contents: write

env:
  TZ: Asia/Shanghai
  BINARY_NAME: atomicserver-amd64-linux

jobs:
  create_release:
    name: Create Release
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Debug Info
        run: |
          echo "GITHUB_REF: ${{ github.ref }}"
          echo "GITHUB_REF_NAME: ${{ github.ref_name }}"
          echo "GITHUB_SHA: ${{ github.sha }}"
          echo "GITHUB_REPOSITORY: ${{ github.repository }}"
          echo "==========================="
          echo "secrets.AGITHUB_TOKEN: ${{ secrets.AGITHUB_TOKEN }}"
          echo "github.ref : ${{ github.ref }}"
          echo "github.ref_name: ${{github.ref_name}}"
          echo "---"
          echo "${{env.BINARY_NAME}}"

      - name: Generate SHA-256
        run: |
          cargo build --release --verbose
          mv target/release/atomic target/release/${{env.BINARY_NAME}}
          pwd
          tree -L 3
          shasum -a 256 target/release/${{env.BINARY_NAME}} | cut -d ' ' -f 1 > target/release/${{env.BINARY_NAME}}.sha256

      - name: Release binary and SHA-256 checksum to GitHub
        uses: softprops/action-gh-release@v2
        with:
          files: |
            target/release/${{env.BINARY_NAME}}
            target/release/${{env.BINARY_NAME}}.sha256
```
