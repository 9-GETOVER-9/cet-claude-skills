# 发布前检查记录

## 已完成的清理

- 删除 `.npm-cache/`。
- 删除 `cet-dashboard/dashboard/node_modules/`。
- 删除 `cet-dashboard/dashboard/dist/`。
- 新增根目录 `.gitignore`。
- 新增 `.gitattributes`，减少 Windows 与 Unix 换行符差异。
- 将乱码文件名修正为 `【先看这里】.md`。
- 更新根目录 `README.md`，补充项目定位、功能、结构、环境要求、隐私说明和已知限制。
- 新增 `GITHUB_PUBLISH_GUIDE.md`。

## 检查结果

- 原项目自带 `npm test` 已通过。
- 原始压缩包中的依赖来自 Windows，因此在 Linux 检查环境中不能直接构建；发布版已删除依赖目录，用户需要在自己的系统执行 `npm install`。
- 未在保留文件中发现常见格式的 API Key、GitHub Token、Private Key 或密码。

## 需要维护者决定的事项

- 是否添加 MIT、Apache-2.0、GPL-3.0 或其他许可证。
- 是否在后续版本中把 skills 的学习数据目录统一改为真正跨平台的可配置路径。
- 是否添加 Dashboard 截图或演示 GIF。
