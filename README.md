# periodic-table-lab-lzcapp

「元素之间 / Element Atlas」懒猫微服（LazyCat）LPK 打包仓库。

- 上游：https://github.com/brin666/periodic-table-lab （React + Vite 双语互动元素周期表）
- 商店：喵喵商店（社区），包名 `community.lazycat.app.element-atlas`
- 构建方式：源码构建（embed 镜像），`build/source.tar.gz` 为上游 commit `c3cfbe2b4c` 源码快照，不上传源码到本仓库、不在 CI 中 git clone
- CI：GitHub Actions（workflow_dispatch 手动触发）调用 `ca-x/lazycat-github-action@v1` 构建并发布到喵喵商店

## 上游无 tag / 无自动更新说明

上游仓库只有一个 commit、无 release/tag，因此 workflow 不配 schedule 自动更新；上游有新提交时，手动替换 `build/source.tar.gz`（更新 `build/SOURCE_SHA`）并手动触发 workflow。

## 上游许可证注意

上游仓库未声明项目级许可证，且明确声明不授予通用复用许可。本仓库仅打包分发以便在懒猫微服上自托管使用，不复制源码内容。
