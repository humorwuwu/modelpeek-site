# ModelPeek 公开页面（App Store 支持 / 营销 / 隐私 / 版权）

页面源码仓库：**https://github.com/humorwuwu/modelpeek-site**（`main` 分支，public）。
GitHub Pages：**https://humorwuwu.github.io/modelpeek-site/**

这是一个纯静态站点，没有构建步骤，直接部署整个目录即可。

| 页面 | 文件 | App Store Connect 字段 |
|---|---|---|
| 营销首页 | `index.html` | Marketing URL（可选） |
| 支持 | `support.html` | Support URL（必填） |
| 隐私政策 | `privacy.html` | Privacy Policy URL（必填） |
| 版权与第三方声明 | `copyright.html` | 版权说明页；App Store 的「版权」字段填 `© 2026 chuanxi wu` |

隐私政策的中文/英文内容也保存在 `docs/appstore/privacy-policy.md`，本页与之同步。

## 已发布的 URL

- 营销首页：`https://humorwuwu.github.io/modelpeek-site/`
- Support URL：`https://humorwuwu.github.io/modelpeek-site/support.html`
- Privacy Policy URL：`https://humorwuwu.github.io/modelpeek-site/privacy.html`
- 版权页：`https://humorwuwu.github.io/modelpeek-site/copyright.html`

GitHub Pages 配置：仓库 `Settings → Pages`，Source 为 `main` 分支的 `/` 根目录；
仓库根目录有 `.nojekyll`，静态文件原样发布。以后推送 `main` 会自动重新构建。

如果以后换自定义域名：在仓库根加 `CNAME`，并在 App Store Connect 里同步改成新域名。

也可以把同一份静态文件部署到自己的服务器/Nginx/Cloudflare Pages/Netlify/Vercel。

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

## 更新流程

项目内的源文件在 `docs/appstore/site/`；本地仓库克隆在 `~/modelpeek-site`。
改完页面后同步并推送：

```sh
rsync -a --exclude '.DS_Store' docs/appstore/site/ ~/modelpeek-site/
git -C ~/modelpeek-site add -A
git -C ~/modelpeek-site commit -m "Update ModelPeek pages"
git -C ~/modelpeek-site push
```

## 合规

- 页面不出现 Autodesk/Navisworks 的暗示关联，只在版权页做事实性格式说明和商标声明。
- 隐私政策明确：不收集、不上传、不出售个人数据；NWD/NWC/NWF 解析在设备本地完成。
- 第三方组件（OCCT、three.js、nwd-reader 及其依赖）在版权页列出，完整许可证随 App 包分发。
- OCCT LGPL 2.1 的合规路径仍需发布者按 `docs/appstore/CHECKLIST.md` 确认。
