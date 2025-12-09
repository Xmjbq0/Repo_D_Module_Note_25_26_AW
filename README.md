# Repo_D_Module_Note_25_26_AW

D模25秋的笔记。注意：不要上传老师上课的手写笔记，只上传整理好的 `.tex` 内容。

## 仓库结构（与 GitHub 保持一致）
- `D-module.tex`：主入口，汇总各周内容并生成最终 PDF。
- `Week1_content.tex`/`Week2_content.tex`/`Week3_content.tex`：每周的正文模块；继续新增周次时按同样命名。
- `ref.bib`：参考文献库。
- `.github/workflows/latex_build.yml`：GitHub Actions 工作流，自动编译 LaTeX 并上传生成的 PDF。
- `.gitignore`：忽略 LaTeX 中间文件和 `*.pdf`，避免把编译产物提交到仓库。
- `.gitattributes`：文本文件自动行尾规范，即`LF`与`CR+LF`之别，规范的是前者即`LF`。
- `D-module.pdf`：本地或 CI 编译产物，默认被 `.gitignore` 忽略，所以仓库主页里没有；不过你在页面上找 Actions ，在 Actions 里面的 artifact 中下载。
- LaTeX 中间文件（如 `.aux/.log/.out/.toc/.bbl/.blg` 等）：由编译产生，已被忽略，无需提交，所以你也在仓库里找不到。

## GitHub Actions（自动编译 PDF）
- 触发：对 `.tex`、`.bib` 或工作流文件的 push / PR，或在 Actions 页面手动 `Run workflow`。
- 编译：使用 `xu-cheng/latex-action@v3`，入口 `D-module.tex`，参数 `-pdf -interaction=nonstopmode -halt-on-error -file-line-error`，自动运行 `pdflatex`。
- 产物：运行结束后上传 `D-module.pdf` artifact，可在对应运行记录里下载。

## 提交/上传流程
1. 克隆：`git clone https://github.com/Xmjbq0/Repo_D_Module_Note_25_26_AW.git`，进入目录。
2. 分支：`git checkout -b feature/<描述>`（如 `feature/week4-notes`），不要直接在 `main` 上改。
3. 编辑：更新相应的 `WeekX_content.tex` 或 `ref.bib`。需要预览可本地跑 `pdflatex D-module.tex`（可能需多跑几次让引用刷新）。
4. 检查：`git status` 确认只有 `.tex/.bib` 等源码被修改，`.gitignore` 会自动屏蔽中间文件和 PDF。
5. 提交：`git add <改动文件>` → `git commit -m "描述本次修改"`。
6. 推送与合并：`git push origin feature/<描述>`，在 GitHub 发起 PR 到 `main`，写清楚改动的周次和要点。CI 会自动编译 PDF，artifact 可供 reviewers 下载查看。
