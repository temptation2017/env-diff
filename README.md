# env-diff

本地对比两段 `.env` / 环境变量文本：新增、删除、变更一目了然。

纯静态单页，打开即可用；解析全在浏览器里完成，**不会上传**任何内容。

## 做什么

把「旧环境」和「新环境」分别贴到左右两侧，立刻看到：

- **新增**：右侧有、左侧没有
- **删除**：左侧有、右侧没有
- **变更**：同一键、值不同
- **相同**：键值一致

可选：忽略注释 / 空行、剥掉 `export ` 前缀、键名大小写敏感、隐藏值（适合截图）。还能一键复制 Markdown 差异报告。

## 怎么打开

### 在线演示

[https://temptation2017.github.io/env-diff/](https://temptation2017.github.io/env-diff/)

### 本地

```bash
git clone https://github.com/temptation2017/env-diff.git
cd env-diff
# 任意静态服务器，或直接用浏览器打开 index.html
python3 -m http.server 8765
# 浏览器访问 http://127.0.0.1:8765
```

也可以直接双击 `index.html`（部分浏览器对 `file://` 下剪贴板权限更严，复制报告可能需本机服务器）。

## 怎么用

1. 左侧贴旧配置，右侧贴新配置（或点「填入示例」）。
2. 按需勾选工具栏选项。
3. 看汇总标签和表格。
4. 需要贴到 PR / Issue 时，点「复制 Markdown 报告」（默认跳过「相同」行）。

## 示例

左侧（本地）：

```env
APP_NAME=DemoShop
DATABASE_URL=postgres://demo:demo@localhost:5432/shop
DEBUG=false
export MAX_UPLOAD_MB=10
```

右侧（预发）：

```env
APP_NAME=DemoShop
DATABASE_URL=postgres://demo:demo@db.internal:5432/shop
DEBUG=true
MAX_UPLOAD_MB=25
REDIS_URL=redis://cache.internal:6379/0
```

开启「忽略 export 前缀」后，会标出 `DATABASE_URL` / `DEBUG` / `MAX_UPLOAD_MB` 变更，以及 `REDIS_URL` 新增。

## 限制

- 只认简单的 `KEY=VALUE` 行；不展开 `$VAR`、不解析多行值、不执行 shell。
- 同名键后者覆盖前者。
- 默认键名不区分大小写（可勾选改为区分）。
- 「隐藏值」只做展示打码，原始文本仍在页面内存里——请勿在不可信场合粘贴真实密钥。

## 后续可改进

- 支持 `.yaml` / JSON 扁平键对比
- 拖放文件导入
- 导出仅「缺失键」清单（给部署检查用）

## License

MIT
