---
title: publish-blog 冒烟测试草稿
date: 2026-05-19
draft: false
slug: blog-pipeline-smoke-test
tags: [元, 测试]
summary: 用来验证 publish-blog.sh 的端到端流程；如果你看到这条线上，说明流水线通了。
math: false
mermaid: false
---
这是一篇用来验证发布流水线的草稿。

它会被 `publish-blog.sh` 处理：

1. 从 wiki/blog-drafts/ 移走
2. 在 wiki/blog-published/ 留一份完整快照（含 source_conversation / wiki_links）
3. 改 frontmatter 把 draft:true 改成 false，并剥掉 source_conversation 和 wiki_links
4. 落到 personal-blog/content/posts/2026-05-19-blog-pipeline-smoke-test.md
5. git commit + push
6. GH Action 跑 Hugo build + 部署

如果你在 https://liang1993.github.io/personal-blog/posts/blog-pipeline-smoke-test/ 看到这段文字，说明流水线 OK。

可以放心删了。
