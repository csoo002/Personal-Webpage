# 部署指南（上传到别人的服务器）

下面给出常用的两种部署方式：SFTP 上传和通过 Nginx 配置并启用 HTTPS（Certbot）。你需要对方服务器的访问凭据或请对方按步骤操作。

1) 使用 SFTP 上传静态文件

- 本地打包（项目小则直接使用当前文件夹）：将 `index.html` 与 `styles.css` 上传到目标服务器的站点目录（例如 `/var/www/example.com/html`）。
- 使用 WinSCP、FileZilla 或命令行 scp：

```bash
# Linux / macOS
scp -r * user@server:/path/to/site/

# Windows (PowerShell)
scp -r * user@server:/path/to/site/
```

2) 使用 SSH + Nginx（在对方服务器有 sudo 权限时）

- 将文件上传到 `/var/www/yourdomain/html`，确保文件权限允许 Nginx 读取：

```bash
sudo chown -R www-data:www-data /var/www/yourdomain/html
sudo chmod -R 755 /var/www/yourdomain
```

- 示例 Nginx 站点配置：

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    root /var/www/yourdomain/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- 重载 Nginx：

```bash
sudo nginx -t
sudo systemctl reload nginx
```

3) 启用 HTTPS（Let's Encrypt + Certbot）

- 在服务器上安装 Certbot 并为 Nginx 自动申请证书：

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

- 若无法在服务器直接运行 Certbot，请考虑由托管方或服务器管理员为你申请并安装证书，或使用 Cloudflare 的 SSL 服务（如果域名使用 Cloudflare）。

如果你愿意，我可以：

- 帮你把当前站点打包并生成上传命令；或
- 指导你和服务器管理员通过 SSH 在服务器上运行 Certbot 并完成 HTTPS。
