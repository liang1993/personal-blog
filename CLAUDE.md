# personal-blog — Hugo + PaperMod 公开博客

## 仓库定位

林彬的个人博客，部署在 GitHub Pages。内容来源：跟 Claude 长对话产生的学习总结、读书笔记、思考反思，经过 humanize 处理后发布。

## 技术栈

- Hugo Extended 0.161+（macOS: `brew install hugo`）
- 主题 PaperMod（`themes/PaperMod`，git submodule）
- 部署 GitHub Pages，构建 .github/workflows/deploy.yml
- 域名 https://liang1993.github.io/personal-blog/

## 目录约定

```
content/posts/      已发布文章，命名 YYYY-MM-DD-slug.md
content/drafts/     本地草稿（.gitignore 屏蔽，不入仓库）
content/about.md    关于页
static/images/      站内图片
archetypes/         hugo new 默认 frontmatter
layouts/            自定义 partials / shortcodes
themes/PaperMod/    submodule，不要直接改主题文件
```

## 写作流程（不在本仓库做）

草稿不在本仓库写，在 personal-wiki（私有）+ 全局 skill 链路完成：

1. 在任何项目跟 Claude 对话
2. `/convo-to-draft` → 草稿落到 `~/liang/personal-wiki/wiki/blog-drafts/`
3. `/humanize-zh <file>` → 去 AI 味
4. 用户手动编辑
5. `/publish-blog <file>` → 自动 cp 到本仓库 `content/posts/`、git commit/push

发布链路 skill 位于 `~/.claude/skills/publish-blog/`，全局可用。

如果手动写一篇（不走 skill），直接在 `content/posts/` 新建 .md 即可。frontmatter 模板见 archetypes/posts.md。

## frontmatter 字段约定

| 字段 | 用途 |
|---|---|
| `title` | 文章标题，中文 |
| `date` | 发布日期 YYYY-MM-DD |
| `draft: false` | 必须为 false 才会上线（archetype 默认 true，要改） |
| `tags: []` | 标签数组 |
| `summary` | 摘要，homepage / RSS 显示 |
| `math: true` | 启用 KaTeX，本文有数学公式时设置 |
| `mermaid: true` | 启用 Mermaid，本文有图表时设置 |
| `ShowToc: true` | 显示目录 |

## 永久链接

`/posts/{slug}/` —— 扁平，不嵌套年月，未来不会被困死。在 `hugo.yaml` 的 `permalinks` 配置。

## 本地预览

```bash
cd /Users/bytedance/liang/personal-blog
hugo server -D            # -D 显示草稿
# 打开 http://localhost:1313
```

## 部署

push 到 main 分支自动触发 `.github/workflows/deploy.yml`，跑 Hugo build → 上传到 gh-pages → GitHub Pages 部署。通常 1-2 分钟绿。

`draft: true` 的文章不会被部署。

## 提交人配置

本仓库已通过 `git config user.email 1027622302liang@gmail.com` 覆盖全局（默认是公司邮箱）。新克隆机器需要重新设置。

## 待办（Phase 2）

- giscus 评论（积累 3-5 篇之后再开）
- 自定义域名（CNAME + DNS，跑通内容再上）
- Goatcounter 访客统计
- 系列文章（taxonomies series 已配，第二篇系列文章时启用）

## 跟 personal-wiki 的关系

- personal-wiki 私有，是知识库 / 草稿源头
- personal-blog 公开，只有定稿
- 两者不互相依赖：publish-blog skill 来回搬，不依赖具体仓库路径
- 但 wiki/blog-published/ 会留每篇 post 的快照 + 来源 frontmatter（source_conversation, wiki_links），方便事后追溯
