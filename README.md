# 个人静态网站（示例）

这是一个最小的静态个人网页示例。包含：

- `index.html`：主页
- `styles.css`：样式

本地预览：

Windows / 其它系统（使用 Python 内置服务器）：

```bash
python -m http.server 8000
# 然后在浏览器打开 http://localhost:8000
```

部署前建议：

- 准备好对方服务器的访问方式（SFTP/SSH/Git）。
- 如果需要 HTTPS，请准备域名并在服务器上使用 Certbot（Let's Encrypt）或由托管方启用证书。
