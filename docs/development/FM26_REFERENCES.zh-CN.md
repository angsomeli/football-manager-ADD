# FMADD：FM26 参考项目

调研日期：2026-10-31。依据公开 README 和列出的源文件；未安装或运行这些项目，未进行真实游戏验证，也未引入其代码或依赖。

| 项目 | 参考价值 | 边界 |
| --- | --- | --- |
| [FMSuperScout](https://github.com/mavarobli/FMSuperScout) | 人员筛选、预设、角色评分、球员比较与发展记录，最适合人员列表设计参考 | BepInEx 读取 + 本地 Web；只读工具。所查根目录没有清晰的项目代码许可证，先参考设计 |
| [fmsave](https://github.com/rhiever/fmsave) | FM26 / 部分 FM27 存档解析；赞助、财务、合同和球场数据，可辅助建立字段字典与离线校验 | MIT；只读解析不证明可写。部分俱乐部与球场关联由赛程推断，不能当成精确所属关系 |
| [fm26rte](https://github.com/poi82999/fm26rte) | Tauri + Rust + React；字段描述、按需读取、修改暂存和提交架构 | 硬编码布局需逐版本验证；未确认根项目许可，不引入代码、偏移或第三方研究材料 |
| [FMMLoader-26](https://github.com/jal-co/FMMLoader-26) | 模组管理、路径检测、备份与恢复交互 | 不是存档编辑器；README 标 CC BY-NC-SA 4.0，但所读 LICENSE 是 GPL v3，需澄清后评估复用 |

查看的实现入口：

- [FMSuperScout 页面](https://github.com/mavarobli/FMSuperScout/blob/main/app/index.html)：球员、员工、候选名单和分析入口。
- [fmsave 球场读取器](https://github.com/rhiever/fmsave/blob/main/src/fmsave/readers/stadiums.py)：按结构特征识别记录；明确区分存储字段与赛程推断关系。
- [fm26rte 后端](https://github.com/poi82999/fm26rte/blob/main/apps/fm26-player-editor/src-tauri/src/lib.rs)：进程连接、字段读写和对象定位。
- [FMMLoader LICENSE](https://github.com/jal-co/FMMLoader-26/blob/main/LICENSE)：与 README 标注存在差异。

额外线索：[fm26-player-export-macos](https://github.com/DadMych/fm26-player-export-macos) 描述了游戏人员表格导出和列预设；它针对 macOS Apple Silicon，不是直接可移植的 Windows 读取方案。

## ADD 的实施顺序

1. 先做人员列表：沿用现有读取服务；所有现有可展示字段登记类型、格式、来源、可用条件与读取成本。支持勾选列、排序、筛选和保存视图，切换卡片复用数据，详情按需加载。
2. 再核对原生字段：区分工具自身商业玩法与 FM 原生赞助合同。同一存档、日期、构建下比较读取结果。
3. 逐字段验证写入：版本门禁、旧值检查、范围检查、写后回读、失败回滚；保存重载及推进日期后仍成立，才能称为持久修改。
4. 单独研究自创球员：需要唯一 ID、人员和球员对象、注册、合同、索引和存档序列化；修改或复制已有球员不等于成功创建新球员。

目前没有确认可直接移植的“赞助 + 球场 + 城市 + 新建球员”完整实现。只读字段不能作为安全写入证据，其他构建的偏移也不能直接套用。

[返回开发计划](PERSONAL_PROJECT_PLAN.zh-CN.md)
