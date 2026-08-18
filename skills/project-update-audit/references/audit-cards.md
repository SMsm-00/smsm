# Project Update Audit Cards

## Minimal Audit Card

```text
【更新前审计卡】

1. 项目名：
这次属于哪个项目？禁止混用哪些项目资料？

2. 本轮动作：
本次只改什么？不改什么？

3. 最新事实源：
以哪些文件、文档、Sync、字段清单或用户确认为准？旧版本哪些结论已废弃？

4. 影响范围：
会影响 PRD、字段清单、API_CONTRACT、前端、后端、提示词、测试数据、文档、部署或权限中的哪些？

5. 是否需要同步：
是否需要输出 Sync to Frontend、Sync to Backend、写入工作流、更新变更记录，或不需要同步？
```

## Compact User-Facing Output

```text
更新前审计：
- 项目边界：本次属于 xxx，不使用 xxx 项目的历史资料。
- 本轮只改：xxx；不改 xxx。
- 最新事实源：以 xxx 为准，旧的 xxx 规则废弃。
- 影响范围：影响 xxx，不影响 xxx。
- 同步判断：需要输出 Sync to Frontend / Sync to Backend / 不需要 Sync。
```

## Trigger Rule For Workflow Documents

```text
当用户提出以下任务时，必须先执行【更新前审计卡】，再开始修改：
- 修改 PRD、字段清单、API_CONTRACT、提示词或项目事实源
- 输出 Sync to Frontend / Sync to Backend
- 修改前端、后端、模拟数据、接口调用或数据模型
- 排查多个项目文件是否符合最新确认范围
- 处理历史数据迁移、权限边界、外部服务接入或生产系统写入

默认只输出 5 行以内审计结论；只有发现冲突、缺少事实源或跨线影响时，才展开说明。
```

## Sync Output Skeleton

```text
Sync to Frontend
本次新增确认：
本次修改：
对前端的影响：
对后端的影响：
对 API_CONTRACT.md 的影响：
不影响的内容：
待确认问题：
```

```text
Sync to Backend
本次新增确认：
本次修改：
对前端的影响：
对后端的影响：
对 API_CONTRACT.md 的影响：
不影响的内容：
待确认问题：
```
