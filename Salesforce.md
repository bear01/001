# Salesforce 测试开发工程师面试题整理

- 生成日期：2026-06-02
- 岗位方向：Software Engineer in Test / QA Automation Engineer / Salesforce QA Engineer / 测试开发工程师
- 业务关键词：CRM、Sales Cloud、Service Cloud、Marketing Cloud、Commerce Cloud、Agentforce、Apex、Flow、Lightning、API、多租户、权限、数据质量、自动化测试、CI/CD、AI 辅助测试
- 说明：以下题目根据公开岗位/面经资料、Salesforce QA 常见考点、Salesforce 平台特性和测试开发通用能力整理，不代表公司官方题库。答案按测试开发工程师面试口径组织，重点突出企业 SaaS、CRM 业务、平台自动化和 AI 质量保障能力。

## 参考来源

- NodeFlair：Salesforce Software Engineer in Test interview questions：https://nodeflair.com/companies/salesforce/interviews/software-engineer-in-test
- Glassdoor：Salesforce QA Engineer interview questions：https://www.glassdoor.com/Interview/salesforce-qa-engineer-interview-questions-SRCH_KO0%2C22.htm
- MockRound：Salesforce QA Engineer interview questions：https://mockround.ai/resources/salesforce-qa-engineer-interview-questions
- Jobaaj Learnings：QA/Test Automation at Salesforce：https://www.jobaajlearnings.com/blog/interview-questions-qa-test-automation-salesforce
- Salesforce Dictionary：QA / Tester interview questions：https://salesforcedictionary.com/interview/qa/apex-test-data-isolation
- Salesforce Developers：Apex Developer Guide：https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/
- Salesforce Developers：Lightning Web Components：https://developer.salesforce.com/docs/platform/lwc/guide
- Salesforce Help：Salesforce Flow：https://help.salesforce.com/s/articleView?id=platform.flow.htm
- Salesforce Help：Profiles, Roles and Permission Sets：https://help.salesforce.com/
- Salesforce AI：Agentforce：https://www.salesforce.com/agentforce/
- Salesforce Trust：https://trust.salesforce.com/
- arXiv：Test Automation Process Improvement in a DevOps Team：https://arxiv.org/abs/2004.06381
- arXiv：System Test Case Design from Requirements Specifications using ChatGPT：https://arxiv.org/abs/2412.03693

## 面试侧重点速览

Salesforce 测试开发面试通常不会只考“会不会写 Selenium”。它会综合考察测试策略、自动化框架、Salesforce 平台理解、Apex/Flow/Lightning 变更影响、权限和数据隔离、多租户 SaaS 稳定性、API 集成、CI/CD、客户业务流程以及 AI/Agentforce 质量保障。回答时要把“业务配置 + 平台元数据 + 自动化验证 + 数据质量 + 权限安全”串起来。

## 一、岗位认知与项目经验

### 1. 你如何理解 Salesforce 测试开发工程师的职责？

**参考答案：** Salesforce 测试开发既要懂测试工程，也要理解 CRM 平台特性。职责包括参与需求评审、设计测试策略、开发 UI/API 自动化、验证 Apex、Flow、Validation Rule、Profile、Permission Set、Role、Sharing Rule、报表和集成接口，并接入 CI/CD。由于 Salesforce 是元数据驱动和多租户平台，测试要关注配置变更、权限边界、数据隔离和跨云业务流程。

**AI 相关加分点：** 可补充用 LLM/RAG 检索需求、对象模型和历史缺陷，生成用例草稿和风险清单，但关键权限和数据断言必须确定性执行。

### 2. 如何介绍一个 Salesforce 自动化测试项目？

**参考答案：** 建议按背景、范围、技术栈、架构、数据、CI 和收益讲。比如负责 Sales Cloud 机会管理自动化，覆盖 Lead 转化、Account/Contact、Opportunity、Quote、审批和报表；使用 Java + Selenium/Playwright + REST API 造数，Page Object 管理页面，数据库/接口断言业务结果，接入 Jenkins 或 GitHub Actions。最终减少人工回归时间并提升核心流程覆盖。

**AI 相关加分点：** 可以说明 AI 用于从用户故事和对象元数据生成候选用例，但进入流水线前要人工审查稳定性和断言。

### 3. Salesforce QA 和普通 Web QA 有什么区别？

**参考答案：** 普通 Web QA 主要围绕固定页面、接口和数据库测试；Salesforce QA 还要理解对象、字段、Record Type、Profile、Permission Set、Role、Sharing、Flow、Apex Trigger、Validation Rule、Page Layout、Lightning Component 和托管包。很多变更是配置或元数据变更，不一定有传统代码 diff，因此需要更强的变更影响分析和权限测试。

**AI 相关加分点：** AI 可读取元数据差异并生成影响面，但权限和共享模型的判断要结合实际用户验证。

### 4. Salesforce 平台最核心的质量风险有哪些？

**参考答案：** 主要包括权限越权、数据可见性错误、Flow 或 Apex Trigger 误触发、Validation Rule 阻断正常流程、集成失败、批量数据处理超限、报表口径错误、页面性能慢、升级后配置失效、客户业务流程中断和 AI 自动化输出不合规。测试要覆盖业务流程、平台限制、数据质量和安全。

**AI 相关加分点：** Agentforce 类功能还要关注 AI 输出事实性、权限边界、提示注入和自动动作安全。

### 5. 如何衡量 Salesforce 测开工作的价值？

**参考答案：** 可用核心业务流程覆盖率、自动化通过率、回归耗时、缺陷发现率、权限缺陷拦截数、CI 反馈时间、数据质量告警、上线事故数和客户影响范围衡量。更重要的是质量信号是否能帮助团队判断一个配置或代码变更是否可发布。

**AI 相关加分点：** AI 工具也要量化收益，例如用例采纳率、失败归因时间下降、误报率和漏测率变化。

## 二、Salesforce 平台测试设计

### 6. 如何测试 Validation Rule？

**参考答案：** 先确认规则目的、适用对象、字段、Record Type、Profile、触发条件和错误提示。测试正常通过、规则触发、边界值、空值、不同用户权限、批量导入、API 调用和 Flow/Apex 触发场景。还要验证错误信息是否清晰，规则是否误伤合法业务。

**AI 相关加分点：** AI 可从规则表达式生成候选边界用例，但要用真实用户和数据验证。

### 7. 如何测试 Profile、Role 和 Permission Set？

**参考答案：** 需要分别验证对象权限、字段权限、记录可见性、页面按钮、报表、API 访问和审批能力。建议构造多个典型用户角色，执行同一业务流程并验证可见、可编辑、不可访问和只读场景。权限测试不能只看页面，还要验证接口和数据层。

**AI 相关加分点：** AI 可生成权限矩阵，但最终应通过自动化模拟不同用户执行。

### 8. 如何测试 Sharing Rule 和数据可见性？

**参考答案：** 先明确 OWD、Role Hierarchy、Sharing Rule、Manual Sharing、Team Sharing 和 Territory Management。测试不同组织结构下记录是否可见、可编辑、可转移。要覆盖创建、转移 owner、角色调整、共享规则变更和缓存延迟。

**AI 相关加分点：** AI 可帮助生成角色树和共享场景，但断言必须由实际查询和页面访问验证。

### 9. 如何测试 Salesforce Flow？

**参考答案：** 覆盖触发条件、输入输出、分支、循环、子 Flow、错误路径、权限、事务回滚、批量处理和版本激活。对 Record-Triggered Flow 要验证创建、更新、删除和字段变化。还要测试 Flow 与 Apex Trigger、Validation Rule 的执行顺序和冲突。

**AI 相关加分点：** AI 可把 Flow 图转为测试路径，但要检查循环、批量和异常路径。

### 10. 如何测试 Apex Trigger？

**参考答案：** 覆盖 before/after insert、update、delete、undelete，单条和批量 200 条，递归、防重复、异常、权限、事务回滚和 governor limits。测试要关注 bulk-safe、查询次数、DML 次数和与 Flow/Validation Rule 的交互。自动化可以通过 API 构造数据并校验结果。

**AI 相关加分点：** AI 可生成 Apex 单测草稿，但 governor limit 和业务断言要人工确认。

### 11. 如何测试 Record Type 和 Page Layout？

**参考答案：** 覆盖不同 Record Type 下字段可见性、必填、默认值、Picklist 值、页面布局、业务流程和权限。测试时使用不同 Profile/Permission Set 用户验证同一对象的差异。还要覆盖 Record Type 变更和历史数据兼容。

**AI 相关加分点：** AI 可根据元数据差异生成矩阵，但要避免组合爆炸，按风险优先。

### 12. 如何测试 Salesforce 报表和仪表盘？

**参考答案：** 验证数据源、过滤条件、分组、汇总、权限、刷新频率、导出、订阅和跨时区。报表测试要建立基准数据，用 SQL/API 或 SOQL 独立计算期望结果。权限场景很重要：用户只能看到有权访问的数据。

**AI 相关加分点：** AI 可生成报表解释和异常摘要，但数据口径必须由确定性计算验证。

## 三、CRM 业务流程测试

### 13. 如何测试 Lead 转化流程？

**参考答案：** 覆盖新建 Lead、字段校验、重复检测、分配规则、状态变更、转化为 Account/Contact/Opportunity、权限、通知和报表。异常包括必填缺失、重复客户、权限不足、Flow 失败和转化后字段映射错误。还要验证转化后数据关系是否正确。

**AI 相关加分点：** AI 可根据客户画像生成测试数据，但不能使用真实客户隐私信息。

### 14. 如何测试 Opportunity 阶段流转？

**参考答案：** 覆盖阶段变更、金额、预计关闭日期、产品、报价、审批、折扣、赢单/输单、权限和历史记录。重点验证阶段约束、必填字段、概率、预测和报表。还要覆盖销售经理和销售代表不同角色的权限。

**AI 相关加分点：** AI 可分析历史商机缺陷，推荐高风险阶段和字段。

### 15. 如何测试 Quote/CPQ？

**参考答案：** 覆盖产品选择、价格规则、折扣、捆绑、合同期限、审批、税费、PDF 生成和同步到 Opportunity。重点关注金额、规则叠加、边界折扣、权限和批量产品。CPQ 场景容易资损，必须有确定性金额基线。

**AI 相关加分点：** AI 可生成组合用例，但价格和折扣必须使用规则引擎或基线数据断言。

### 16. 如何测试 Case 管理流程？

**参考答案：** 覆盖 Case 创建、队列分配、SLA、升级、状态流转、邮件通知、知识库推荐、关闭和客户反馈。异常包括重复 Case、超时升级、权限不足、邮件失败和自动化规则冲突。Service Cloud 场景要关注客户体验和 SLA 指标。

**AI 相关加分点：** 对 AI 客服助手，要测试推荐答案准确性、权限边界和人工接管。

### 17. 如何测试审批流程？

**参考答案：** 覆盖提交、审批人选择、多人审批、拒绝、撤回、重新提交、代理审批、超时和通知。验证不同金额、折扣、地区和角色触发的审批路径。还要确保审批期间记录锁定和权限符合预期。

**AI 相关加分点：** AI 可推荐审批风险，但最终审批链路必须由规则和权限驱动。

### 18. 如何测试数据导入和批量处理？

**参考答案：** 覆盖 Data Loader/API 批量导入、字段映射、重复数据、必填缺失、Validation Rule、Trigger、Flow、批量 200 条和大数据量。重点验证错误行报告、事务处理、性能和 governor limit。批量场景常能发现单条测试发现不了的问题。

**AI 相关加分点：** AI 可生成批量数据变体，但要确保 bulk-safe 和隐私脱敏。

## 四、自动化框架与 CI/CD

### 19. 如何设计 Salesforce UI 自动化框架？

**参考答案：** 框架应包含 Page Object、稳定定位器、用户切换、数据工厂、环境配置、截图日志、报告、失败重试和 CI 集成。Salesforce Lightning 页面动态性强，UI 自动化要控制数量，优先覆盖关键用户路径。更多业务校验可以下沉到 API 和 SOQL。

**AI 相关加分点：** AI 生成 UI 脚本时常用脆弱选择器，必须人工优化定位和等待策略。

### 20. 如何设计 Salesforce API 自动化？

**参考答案：** 使用 REST/SOAP/Bulk API 构造数据、执行操作、查询结果和清理数据。框架要处理 OAuth、环境、对象元数据、字段、错误码和数据隔离。API 自动化适合验证业务规则、权限、集成和批量场景，但不能完全替代 UI 体验测试。

**AI 相关加分点：** AI 可根据对象元数据生成 API 用例，但权限和字段断言要明确。

### 21. 如何做测试数据管理？

**参考答案：** 建议用数据工厂按对象关系生成 Account、Contact、Lead、Opportunity、Quote、Case 等数据，并记录唯一标识和清理策略。测试数据要考虑 Record Type、必填字段、Picklist、Lookup、权限和 Flow/Trigger 依赖。固定共享数据容易导致并发冲突。

**AI 相关加分点：** AI 可生成业务化数据，但要避免真实客户信息，并能识别元数据依赖。

### 22. 如何把 Salesforce 自动化接入 CI/CD？

**参考答案：** PR 阶段跑静态检查、Apex 单测和快速 API 冒烟；合并后跑核心业务回归；发布前跑 UI 关键路径、权限矩阵和集成测试。流水线要支持 scratch org/sandbox、元数据部署、测试数据初始化、报告和失败通知。质量门禁应区分关键失败和非关键失败。

**AI 相关加分点：** 用 AI 根据元数据 diff 推荐回归范围，但关键权限和资金场景不能省略。

### 23. 如何治理 flaky 自动化用例？

**参考答案：** 常见原因包括 Lightning 页面异步加载、数据冲突、权限状态、环境慢、集成依赖、脚本定位不稳定和测试污染。治理方式包括 API 造数、稳定等待、数据隔离、减少 UI 依赖、失败截图、重试限制和 owner 机制。长期要统计 flaky 来源并改造。

**AI 相关加分点：** AI 可聚类失败日志和截图，辅助定位是否为页面等待、数据或权限问题。

### 24. 如何设计质量看板？

**参考答案：** 看板应展示自动化通过率、核心流程覆盖、权限缺陷、元数据变更风险、Apex 单测覆盖、Flow 失败、集成错误、数据质量、CI 耗时和线上告警。对企业 SaaS，还应按客户影响、业务对象和发布版本拆分。

**AI 相关加分点：** AI 可生成质量日报和风险摘要，但原始指标要可追溯。

## 五、集成、数据质量与安全

### 25. 如何测试 Salesforce 与外部系统集成？

**参考答案：** 覆盖接口契约、鉴权、字段映射、同步方向、失败重试、幂等、延迟、错误码、数据补偿和监控。常见集成包括 ERP、营销系统、客服系统、支付和数据仓库。测试要验证双方数据一致，并保留 trace 和关联 ID。

**AI 相关加分点：** AI 可分析集成日志并推荐根因，但要用数据对账确认。

### 26. 如何测试数据质量？

**参考答案：** 数据质量包括完整性、准确性、一致性、唯一性、及时性和可追溯性。Salesforce 场景要关注重复客户、字段缺失、Picklist 错误、关系断裂、历史数据迁移和报表口径。测试方式包括 API/SOQL 校验、数据质量规则、报表对账和异常告警。

**AI 相关加分点：** 用异常检测发现字段分布漂移、重复率突增和数据同步延迟。

### 27. 如何测试多租户隔离？

**参考答案：** 多租户隔离要验证不同 org、客户、用户和权限边界的数据不能互相访问。测试覆盖 API、页面、报表、缓存、搜索索引、异步任务和日志。隔离缺陷严重度很高，需要明确的负向用例和审计。

**AI 相关加分点：** AI/Agentforce 读取企业知识时也必须严格遵守租户和权限边界。

### 28. 如何测试安全和隐私？

**参考答案：** 覆盖认证、授权、越权、字段级权限、共享规则、API 权限、输入校验、XSS、CSRF、日志脱敏、审计和数据保留。CRM 系统承载客户、销售和服务数据，安全测试要重点保护 PII、商业机会和合同信息。

**AI 相关加分点：** 对 AI 助手要额外测试提示注入、敏感数据泄露和越权检索。

### 29. 如何测试性能？

**参考答案：** 覆盖页面加载、SOQL 查询、Apex 执行、Flow 执行、报表、批量导入、API 并发和集成吞吐。要关注 P95/P99、超时、governor limits、缓存和大数据量。性能测试应结合基准数据和真实业务模型。

**AI 相关加分点：** AI 可分析慢查询和日志，但优化建议要通过 Explain 和压测验证。

### 30. 如何测试可用性和可靠性？

**参考答案：** 结合 Salesforce Trust 状态、环境监控、发布灰度、错误率、API 限制、集成失败和业务成功率。测试要覆盖依赖服务异常、网络失败、异步任务堆积、批量处理失败和恢复。可靠性不仅看服务在线，还看客户流程是否能完成。

**AI 相关加分点：** AI 可做异常检测和告警摘要，帮助快速识别影响范围。

## 六、编码、SQL/SOQL 与排障

### 31. 如何写 SOQL 查询最近修改的 Opportunity？

**参考答案：** 可以按 LastModifiedDate 降序查询，例如选择 Id、Name、StageName、Amount、LastModifiedDate，并使用 LIMIT 控制数量。如果要按 Account 分组取最新商机，需要结合子查询或外部数据处理。测试时要注意权限、字段可见性和大数据量限制。

**AI 相关加分点：** AI 可生成 SOQL 草稿，但要检查字段权限和性能。

### 32. 如何排查 Flow 更新后大量 Case 创建失败？

**参考答案：** 先确认失败范围、时间、用户、Record Type 和错误信息。再检查 Flow 新版本、Validation Rule、必填字段、权限、Apex Trigger、集成依赖和日志。快速止血可回退 Flow 版本或关闭相关自动化。事后补充该 Flow 的路径测试和批量回归。

**AI 相关加分点：** AI 可汇总失败日志和最近元数据变更，生成排查时间线。

### 33. 如何排查 API 调用突然失败？

**参考答案：** 先看错误码、认证、Token、权限、API 限制、字段变更、对象权限、网络和下游系统。再按调用方、时间、对象和版本拆分。若是字段或权限变更导致，需要回滚或兼容，并补充契约测试。

**AI 相关加分点：** AI 可聚类错误响应，但根因要通过日志和配置变更确认。

### 34. 如何测试一个去重算法？

**参考答案：** 以客户去重为例，覆盖完全相同、姓名相同电话不同、邮箱大小写、空字段、模糊匹配、国际号码、公司名简称和大数据量。要明确去重规则和优先级，避免误合并不同客户。输出应可解释并支持人工复核。

**AI 相关加分点：** AI 可做模糊匹配候选，但合并客户这种高风险动作需要规则和人工确认。

## 七、Agentforce、AI 与智能质量

### 35. 如何测试 Agentforce 智能代理？

**参考答案：** 覆盖意图识别、知识检索、工具调用、业务动作、权限、失败兜底、人工接管和审计。比如客服代理创建 Case 或回复客户时，要验证它只能访问授权数据，输出准确，动作可追溯。还要测试多轮对话、上下文变化和异常输入。

**AI 相关加分点：** 重点测试 RAG 权限过滤、提示注入、幻觉和自动动作安全。

### 36. 如何测试 AI 推荐的销售下一步动作？

**参考答案：** 验证推荐是否基于授权数据、是否符合业务规则、是否可解释、是否能提升销售流程。测试要覆盖不同客户阶段、数据缺失、历史活动、地区差异和异常输入。不能让 AI 推荐违反合规或泄露客户信息的动作。

**AI 相关加分点：** 评估不仅看准确率，也要看采纳率、业务效果和风险样本。

### 37. 如何测试 RAG 系统？

**参考答案：** 关注检索、重排、生成和引用。测试召回率、权限过滤、上下文截断、答案事实性、引用正确性、无答案处理和知识库更新延迟。企业 SaaS 场景最关键的是租户隔离和字段级权限。

**AI 相关加分点：** 权限过滤必须是硬断言，不能靠模型“自觉不回答”。

### 38. 如何测试提示注入？

**参考答案：** 构造恶意邮件、知识库文章、Case 描述、网页或聊天内容，诱导 AI 忽略系统指令、泄露数据或执行危险动作。测试直接注入、间接注入、多轮对话和工具调用链。验证系统是否有指令隔离、权限控制、输出过滤和审计。

**AI 相关加分点：** 提示注入样本库需要持续更新，并接入安全回归。

### 39. 如何测试 AI 生成测试用例的系统？

**参考答案：** 评估需求覆盖率、边界覆盖率、重复率、错误率、可执行率、采纳率和缺陷发现率。输入包括用户故事、对象元数据、Flow、Apex、历史缺陷和权限矩阵。输出要能追溯到需求点，并经过规则校验、人工评审和 CI 执行。

**AI 相关加分点：** 用 RAG 引入团队测试规范和 Salesforce 元数据，可提高生成质量。

### 40. 如何测试 AI 生成代码或 Apex 单测？

**参考答案：** 验证代码是否编译、单测是否通过、边界条件是否覆盖、是否违反 governor limits、是否存在安全漏洞、是否可维护。AI 生成的 Apex 测试还要检查测试数据隔离、批量场景和断言是否有意义。不能只追求覆盖率。

**AI 相关加分点：** AI 生成代码进入仓库前必须经过代码审查、静态扫描和真实执行。

## 八、系统设计与开放题

### 41. 设计一个 Salesforce 自动化测试平台。

**参考答案：** 平台包括用例管理、对象元数据读取、数据工厂、环境管理、用户权限矩阵、API/UI 执行、报告、失败归因、CI/CD、质量看板和审计。支持 scratch org/sandbox 初始化、元数据部署、测试数据清理和结果趋势分析。目标是把业务流程、平台元数据和自动化执行连接起来。

**AI 相关加分点：** AI 可生成用例草稿、风险回归推荐和失败摘要，但所有输出要可追溯。

### 42. 设计一个权限回归测试系统。

**参考答案：** 系统维护角色、Profile、Permission Set、对象、字段和记录级可见性矩阵。每次权限或共享规则变更后，自动使用不同用户执行页面、API 和报表访问，验证正向和负向权限。结果要能定位到具体权限配置。

**AI 相关加分点：** AI 可分析权限 diff 并推荐回归用户组合。

### 43. 设计一个 Flow 变更影响分析系统。

**参考答案：** 系统读取 Flow 元数据、触发对象、字段、分支、子 Flow 和关联 Apex/Validation Rule，生成影响对象、字段和业务流程列表。再结合历史缺陷和自动化覆盖，推荐需要回归的用例。发布后监控 Flow 错误和业务指标。

**AI 相关加分点：** LLM 可把复杂 Flow 转成自然语言路径摘要，方便评审。

### 44. 线上客户反馈某些用户看不到商机，你如何排查？

**参考答案：** 先确认用户、商机、时间和操作路径，再检查 Profile、Permission Set、Role、OWD、Sharing Rule、Owner、Team、Territory、字段权限和最近配置变更。用管理员和受影响用户分别验证页面、API 和报表。若是共享规则变更导致，快速回滚或补充共享。

**AI 相关加分点：** AI 可汇总权限配置和最近变更，但权限结论要通过实际访问验证。

### 45. 设计一个 Agentforce 安全评测平台。

**参考答案：** 平台包括评测集、权限矩阵、知识库、提示注入样本、工具调用记录、自动评分、人工标注、审计和上线门禁。评测维度包括事实性、权限边界、敏感数据泄露、危险动作、引用正确性、人工接管和延迟。结果要可追溯到模型、提示、数据和策略版本。

**AI 相关加分点：** 安全评测要持续接收线上反馈和新攻击样本。

### 46. 如果入职 Salesforce 测试开发团队，前三个月如何开展工作？

**参考答案：** 第一个月熟悉产品云、对象模型、权限体系、发布流程、测试框架和质量指标；第二个月接手核心模块，补齐高风险自动化、治理 flaky 或完善数据工厂；第三个月推动一个可量化改进，例如缩短回归时间、提升权限回归覆盖或建设元数据变更风险看板。回答要体现平台理解、客户影响和工程落地。

**AI 相关加分点：** 可把 AI 辅助元数据影响分析、用例生成或失败归因作为增效项目，但先从低风险场景试点。

## AI 相关加分点汇总

- 用 LLM/RAG 结合用户故事、对象元数据、Flow、Apex、历史缺陷和权限矩阵生成候选用例。
- 对 Agentforce 和 AI 助手重点测试权限边界、RAG 检索、提示注入、幻觉、自动动作安全和人工接管。
- 用 AI 做失败日志摘要、相似缺陷检索、元数据变更影响分析和质量日报。
- 对 AI 生成 Apex、Flow 或自动化脚本，必须做代码审查、静态扫描、单测、CI 执行和业务断言验证。
- AI 工具接入测试平台时要有脱敏、租户隔离、权限控制、审计和可追溯证据。

## 复习建议

1. 复习 Salesforce 基础：对象、字段、Record Type、Profile、Permission Set、Role、Sharing、Flow、Apex、Lightning。
2. 准备一个自动化框架项目，重点讲数据工厂、API/UI 分层、权限测试、CI/CD、报告和失败归因。
3. 熟悉 CRM 流程：Lead、Account、Contact、Opportunity、Quote、Case、审批、报表和集成。
4. 重点练习权限矩阵、Flow/Apex 变更影响、批量数据、governor limits 和多租户隔离。
5. 准备 AI 测试话题：Agentforce、RAG、提示注入、AI 生成用例、AI 生成代码和企业数据安全。
6. 回答开放题时按“业务对象 -> 权限/数据风险 -> 自动化方案 -> CI 门禁 -> 线上监控”的结构展开。
