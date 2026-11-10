# ModelPeek 公开页面（App Store 支持 / 营销 / 隐私 / 版权）

页面源码已存储在私有库：
**https://github.com/humorwuwu/modelpeek-site**（`main` 分支，private）。

这是一个纯静态站点，没有构建步骤，直接部署整个目录即可。

| 页面 | 文件 | App Store Connect 字段 |
|---|---|---|
| 营销首页 | `index.html` | Marketing URL（可选） |
| 支持 | `support.html` | Support URL（必填） |
| 隐私政策 | `privacy.html` | Privacy Policy URL（必填） |
| 版权与第三方声明 | `copyright.html` | 版权说明页；App Store 的「版权」字段填 `© 2026 chuanxi wu` |

隐私政策的中文/英文内容也保存在 `docs/appstore/privacy-policy.md`，本页与之同步。

## 部署后要填的 URL

假设部署在 `https://example.com/modelpeek/`：

- Support URL：`https://example.com/modelpeek/support.html`
- Marketing URL：`https://example.com/modelpeek/`
- Privacy Policy URL：`https://example.com/modelpeek/privacy.html`

如果部署在 GitHub Pages（仓库公开时）：

1. Settings → Pages → Source 选 `Deploy from a branch`；
2. 分支 `main`，目录选 `/docs`；
3. 页面会是 `https://<用户名>.github.io/<仓库名>/appstore/site/`，
   Support URL 对应 `.../appstore/site/support.html`。
   想要更短的路径，可把 `site/` 的内容放到 `gh-pages` 分支根目录。

也可以直接上传到自己的服务器/Nginx/Cloudflare Pages/Netlify/Vercel。

> 注意：当前仓库是 **private**。GitHub Pages 的私有库发布需要 GitHub Pro/Team/Enterprise
> 等支持私有 Pages 的计划；免费账号的 Pages 只对公开库开放。若要保持仓库私有，建议用
> Cloudflare Pages / Netlify / Vercel 连接这个私有库（不需要把仓库改成公开），或部署到
> 自己的服务器。启用任何公开托管都会让这些页面公开到互联网——App Store 的支持 URL 和
> 隐私政策 URL 本来就需要公开。

## 需要确认/替换的内容

- **联系邮箱**：页面里统一用 `humorwu@163.com`。如需更换，搜索并替换
  `support.html`、`privacy.html`、`copyright.html`。
- **版权人**：页面写的是 `© 2026 chuanxi wu`。如果要用公司名，统一替换。
- **App Store 链接**：`https://apps.apple.com/app/id6832817884`，审核通过后生效；
  页面底部已注明“审核通过后生效”。
- **营销截图**：`assets/` 里的图来自自建示例模型 `sample.step`，不是现场工程模型；
  重新生成用 `python3 scripts/make_sample_model.py`，再从 `release/ios/store/screenshots/`
  选图缩放。

## 本地预览

```sh
python3 -m http.server 8080 --directory docs/appstore/site
open http://127.0.0.1:8080/
```

不需要网络；页面没有外部字体、脚本或 CDN 依赖。

## 合规

- 页面不出现 Autodesk/Navisworks 的暗示关联，只在版权页做事实性格式说明和商标声明。
- 隐私政策明确：不收集、不上传、不出售个人数据；NWD/NWC/NWF 解析在设备本地完成。
- 第三方组件（OCCT、three.js、nwd-reader 及其依赖）在版权页列出，完整许可证随 App 包分发。
- OCCT LGPL 2.1 的合规路径仍需发布者按 `docs/appstore/CHECKLIST.md` 确认。
