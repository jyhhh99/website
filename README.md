# 公式转换台 FormulaDesk

把公式截图，或任意写法的公式文本，转换成 Overleaf 可编译的 LaTeX，以及可以直接粘贴进 Word 的公式（MathML）。

整个网站只有一个静态文件 `index.html`，不需要服务器、数据库或后端。

## 两种识别模式

| 模式 | 费用 | 数据去向 | 适合 |
|---|---|---|---|
| **本地免费** | 免费 | 图片只在用户自己的浏览器里处理 | 印刷体、清晰截图、单个公式 |
| **AI 模式** | 用户自己的 API 额度 | 浏览器直接发给用户选的服务商 | 手写、整页多公式、非 LaTeX 文本转换 |

- 本地模式使用开源模型 [Texo / FormulaNet](https://github.com/alephpi/Texo)（约 80 MB，第一次使用时下载，之后保存在浏览器缓存里），通过 [Transformers.js](https://github.com/huggingface/transformers.js) 在浏览器里运行。
- AI 模式支持 Anthropic Claude、OpenAI、Google Gemini，以及任何 OpenAI 兼容接口（通义千问、智谱、OpenRouter、硅基流动等）。密钥只存在用户自己的浏览器里，本站接触不到。

## 发布到网上（任选一种）

### A. Netlify Drop（最快，约 2 分钟）
1. 打开 https://app.netlify.com/drop 并登录（可以用 GitHub 或邮箱注册）。
2. 把整个 `public` 文件夹拖进网页。
3. 得到一个 `xxx.netlify.app` 网址，在 Site settings 里可以改成好记的名字。

### B. GitHub Pages（免费，方便以后更新）
1. 在 GitHub 新建一个公开仓库，比如 `formuladesk`。
2. 上传 `index.html`、`README.md` 和 `LICENSE`。
3. 仓库 Settings → Pages → Source 选 `main` 分支、根目录 `/`，保存。
4. 一两分钟后网址是 `https://<你的用户名>.github.io/formuladesk/`。

### C. Cloudflare Pages
在 https://pages.cloudflare.com 选「直接上传」，上传这个文件夹即可。

> 推荐通过 `https://` 网址访问。直接双击打开 `index.html` 也能用，但识别时页面会短暂卡顿。

## 访问说明
- 模型下载源默认「自动选择」：同时探测 Hugging Face、GitHub、hf-mirror.com，用最先连通的那个，失败了自动换下一个。hf-mirror.com 只在中国大陆能连上。
- 网站本身托管在 Netlify 或 GitHub Pages 时，在中国大陆访问可能偏慢。
- AI 模式下，部分服务商不允许浏览器直接调用（CORS 限制），页面会提示「连不上服务商」，换一家即可。Anthropic、OpenAI、Gemini、OpenRouter 都支持浏览器直接调用。

## 许可协议
本地识别模型 Texo / FormulaNet 采用 **AGPL-3.0** 协议。本网站调用了该模型，所以按 AGPL-3.0 公开发布，源码就是这个 `index.html`。公开部署时请保留页脚的署名链接。
