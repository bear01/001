# GitLab 测试开发工程师面试题

## 公司名

GitLab

## 岗位方向

测试开发工程师 / SDET / QA Automation Engineer / DevSecOps 与 AI 工程平台质量方向

## 资料来源与整理依据

- [GitLab DevSecOps Platform Docs](https://docs.gitlab.com/devsecops/)
- [GitLab CI/CD Documentation](https://docs.gitlab.com/ci/)
- [Application Security Testing](https://docs.gitlab.com/user/application_security/)
- [Static Application Security Testing](https://docs.gitlab.com/user/application_security/sast/)
- [Code Quality](https://docs.gitlab.com/ci/testing/code_quality/)
- [GitLab Duo](https://docs.gitlab.com/user/gitlab_duo/)
- [GitLab Duo Agent Platform](https://docs.gitlab.com/user/duo_agent_platform/)
- [GitLab Observability](https://docs.gitlab.com/operations/observability/observability/)
- [Incident Management](https://docs.gitlab.com/operations/incident_management/)
- 公开候选人面经中常见的 GitLab / DevSecOps / CI/CD 平台测试开发方向：Ruby/Go/JavaScript、API 自动化、流水线调度、安全扫描、Runner、权限模型、AI Agent、质量门禁和行为面。

> 说明：以下题目不是 GitLab 官方题库，而是结合公开资料、DevSecOps 平台产品形态和测试开发岗位能力模型整理的高频准备题与模拟题。

## 面试画像

GitLab 的核心场景覆盖代码托管、Merge Request、Issue、CI/CD、Runner、Package/Container Registry、DevSecOps 安全扫描、DORA 指标、GitLab Duo、Agent Platform、Observability 和 Incident Management。测试开发工程师需要证明自己能在复杂协作流程、海量流水线、安全扫描、AI 辅助开发、权限治理和生产稳定性场景中建立可扩展的自动化测试体系。

## 题目分类

### 一、岗位理解与 DevSecOps 质量

### 1. 你如何理解 GitLab 测试开发工程师的核心价值？

参考答案：核心价值是保障从代码提交、评审、构建、测试、安全扫描、部署到监控响应的全链路可靠。GitLab 是 DevSecOps 平台，质量问题可能导致流水线阻塞、错误合并、权限越界、安全漏洞漏检或 AI Agent 误操作。测试开发要把研发流程风险转化为自动化回归、契约测试、安全测试、性能基线和发布门禁。

### 2. DevSecOps 平台测试和普通业务系统测试有什么区别？

参考答案：普通业务系统更关注业务交易，DevSecOps 平台还要覆盖代码协作、CI/CD 调度、权限、审计、安全扫描、制品管理、Runner 执行环境和开发者体验。测试对象包括 API、Web、后台任务、队列、Git 操作、Pipeline YAML、安全报告和第三方集成。质量目标是让团队能安全、快速、可追溯地交付软件。

### 3. GitLab 面试中为什么会重视 CI/CD？

参考答案：CI/CD 是 GitLab 的核心能力之一，连接代码、测试、安全和部署。测试开发需要理解 pipeline graph、job、stage、artifact、cache、rules、needs、environment、runner 和失败重试。很多质量问题出现在调度、并发、缓存、制品、权限和外部执行环境中。

### 4. 如何衡量 GitLab 平台质量？

参考答案：可以从 pipeline 成功率、平均排队时间、job 执行稳定性、MR 合并效率、API 错误率、页面性能、安全扫描准确性、Runner 可用性、告警响应时间和 AI 功能采纳质量衡量。质量指标要能按项目、组、版本、功能和客户类型下钻。

### 5. 面试中如何体现自己适合 GitLab 这类工程平台？

参考答案：可以强调三类能力：懂研发流程，如 Git、MR、CI/CD、制品和部署；懂平台质量，如 API、权限、异步任务、性能、可观测性和测试平台；懂安全与 AI，如 SAST、Secret Detection、Duo、Agent 和权限边界。最好用项目案例说明如何把研发效率和质量门禁结合起来。

### 6. 如果一个功能让 MR 合并变慢，你会如何评估风险？

参考答案：先分解变慢位置，是页面渲染、权限计算、diff 生成、pipeline 状态、approval 校验还是后台任务。再用真实项目规模、不同文件数、不同 pipeline 数和不同权限角色压测。指标包括 P95/P99、数据库查询、缓存命中、前端耗时和用户感知延迟。

### 二、CI/CD、Runner 与制品管理

### 7. 如何测试 GitLab CI/CD pipeline？

参考答案：覆盖 YAML 解析、stage 顺序、rules、needs、variables、artifacts、cache、manual job、retry、allow_failure、child pipeline 和环境部署。测试要验证 pipeline graph、job 状态、日志、制品、权限和失败恢复。复杂 YAML 应使用 fixture 和端到端样例做回归。

### 8. 如何测试 Runner 调度？

参考答案：构造不同 runner tag、executor、并发限制、项目权限、队列积压和 runner 离线场景，验证 job 是否被正确分配。还要测试取消、超时、重试、日志流、artifact 上传和 runner 版本兼容。调度测试要关注公平性和租户隔离。

### 9. 如何测试 pipeline cache？

参考答案：覆盖 cache key、fallback key、分支隔离、共享缓存、缓存过期、并发写入和缓存损坏。断言包括 job 是否命中缓存、是否正确回退、是否污染其他分支或项目。缓存能提升速度，但错误缓存会造成构建不一致。

### 10. 如何测试 artifacts？

参考答案：覆盖上传、下载、过期、权限、大小限制、路径匹配、report artifacts 和失败 job artifacts。测试要验证 MR 页面、pipeline 页面和 API 是否能正确读取 artifact。敏感制品要验证权限和过期清理，避免泄露。

### 11. 如何测试 pipeline variables？

参考答案：覆盖项目、组、实例、环境、protected、masked、file variable 和 job 级变量优先级。负向测试包括变量泄露到日志、无权限用户读取变量、fork pipeline 使用 protected variable 和变量覆盖。敏感变量必须脱敏且可审计。

### 12. 如何测试环境部署和回滚？

参考答案：覆盖 review app、staging、production、manual deploy、approval、environment status、rollback 和 stop environment。验证部署记录、权限、审计、artifact 版本和监控链接。部署测试要和 CI/CD、权限、环境变量和基础设施集成测试结合。

### 13. 如何测试 merge train？

参考答案：构造多个 MR、冲突变更、pipeline 成功失败、重新排队和取消场景，验证合并顺序、临时合并提交和最终目标分支状态。merge train 的核心是保护主分支稳定性，测试要防止 race condition 和错误合并。

### 14. 如何测试 GitLab Pages 或静态站点部署？

参考答案：覆盖构建、artifact、域名、TLS、权限、缓存、预览和删除。测试要验证页面内容、访问控制、构建失败提示和安全 header。对于大规模静态站点，还要关注发布延迟和 CDN 缓存刷新。

### 三、DevSecOps、安全扫描与质量门禁

### 15. 如何测试 SAST 集成？

参考答案：准备不同语言、框架、漏洞样本和无漏洞样本，验证扫描触发、报告格式、漏洞定位、严重性、误报、去重和 MR 展示。SAST 结果应出现在 pipeline、MR 和安全 dashboard 中。还要测试 analyzer 版本升级对结果的影响。

### 16. 如何测试 Secret Detection？

参考答案：构造真实格式 token、假 token、历史提交、二进制文件、压缩文件和允许列表，验证识别、定位、严重性和误报处理。测试要确保 secret 不被打印到 job log 或测试报告。对已泄露 secret，应验证撤销建议和审计记录。

### 17. 如何测试 Dependency Scanning？

参考答案：准备不同包管理器、锁文件、传递依赖、漏洞数据库更新和私有依赖场景。断言包括 CVE、严重性、修复版本、路径、license 和 MR 注释。还要验证漏洞数据库更新后是否触发结果变化。

### 18. 如何测试 Container Scanning？

参考答案：准备不同基础镜像、包版本、漏洞、镜像 registry 权限和多架构镜像，验证扫描、报告、修复建议和镜像层定位。负向场景包括 registry 鉴权失败、镜像不存在、超大镜像和扫描超时。扫描失败应给出可诊断信息。

### 19. 如何测试 DAST？

参考答案：准备测试应用、登录流程、爬取范围、排除路径、攻击样本和网络异常，验证漏洞识别、误报、报告、认证和超时。DAST 运行在动态环境中，测试要关注隔离环境和不可破坏生产数据。结果要能回到 MR 或安全 dashboard。

### 20. 如何测试 Code Quality？

参考答案：准备不同 lint 工具输出、code climate 格式、重复问题、修复问题和 MR diff，验证报告解析、MR 展示和质量门禁。Code Quality 测试重点是报告格式兼容、增量问题展示和 developer experience。工具失败时要有清晰错误。

### 21. 如何设计安全扫描质量门禁？

参考答案：门禁应按严重性、漏洞类型、是否新增、是否可利用和业务例外分级。测试要覆盖阻断、允许、例外审批、过期例外和审计。门禁不能简单阻断所有问题，否则会降低开发效率；也不能让高危漏洞静默进入主分支。

### 22. 如何测试 Vulnerability Management？

参考答案：覆盖漏洞创建、去重、状态流转、dismiss、confirm、resolve、issue 关联、MR 修复和 dashboard 统计。测试要验证同一漏洞在不同分支、不同扫描器和不同版本中的合并逻辑。审计和权限也很关键。

### 四、GitLab Duo、AI Agent 与安全

### 23. GitLab Duo 的测试重点是什么？

参考答案：GitLab Duo 涉及代码建议、Chat、解释、测试生成、MR 摘要、漏洞解释和 Agent 能力。测试重点包括准确性、上下文权限、代码质量、安全性、延迟、成本和用户体验。AI 输出必须基于用户有权访问的项目数据，不能泄露私有代码或变量。

### 24. 如何测试 AI 代码建议？

参考答案：准备不同语言、框架、上下文长度和安全敏感场景，评估补全是否可编译、符合风格、通过测试且不引入漏洞。还要检查是否复制敏感代码、生成不安全依赖或泄露 secret。指标包括接受率、编译通过率、测试通过率和安全扫描结果。

### 25. 如何测试 AI 生成测试？

参考答案：选择函数、组件、API 和边界场景，验证生成测试是否能运行、是否有有效断言、是否覆盖异常路径、是否稳定。不能只看生成数量，要看测试是否能发现缺陷。生成测试应进入代码 review 和 CI。

### 26. 如何测试 Duo Agent Platform？

参考答案：Agent 测试要覆盖任务理解、上下文检索、工具调用、权限、审批、回滚、审计和成本限制。构造无权限项目、恶意 issue、prompt injection、循环任务和工具失败场景。Agent 不能因自然语言指令绕过 GitLab 权限模型。

### 27. 如何测试 AI 对安全漏洞的解释？

参考答案：准备 SAST、Dependency、Secret 和 Container 扫描结果，验证 AI 是否准确解释漏洞、影响、修复建议和相关代码。测试要检查幻觉、错误严重性、过度自信和错误修复。高风险建议应引用实际扫描结果和代码位置。

### 28. 如何测试 prompt injection？

参考答案：在 issue、MR 描述、代码注释、README 和 pipeline log 中加入恶意指令，验证 Duo 或 Agent 是否忽略不可信内容中的越权指令。测试要覆盖泄露变量、绕过权限、执行命令和修改安全配置。AI 系统应区分用户内容、系统规则和工具结果。

### 29. 如何测试 AI 上下文权限？

参考答案：构造不同角色、项目可见性、group 权限、fork、protected branch 和 confidential issue，验证 AI 只能访问授权上下文。不能因为 AI 需要上下文而扩大权限。测试应覆盖检索、缓存、日志和模型输入输出全链路。

### 30. 如何评估 AI 功能上线效果？

参考答案：指标包括任务成功率、用户采纳率、错误率、人工修改成本、代码质量、安全问题、延迟、成本和投诉。离线评测与线上指标要结合，避免只看 demo 成功。对高风险 AI 功能需要灰度、反馈回流和回滚。

### 五、API、权限与协作流程

### 31. 如何测试 GitLab API？

参考答案：覆盖鉴权、分页、过滤、排序、错误码、幂等、限流、GraphQL/REST 一致性和权限。关键资源包括 projects、groups、users、issues、MR、pipelines、jobs、artifacts 和 security findings。自动化应验证 API、Web UI 和数据库状态一致。

### 32. 如何测试权限模型？

参考答案：构造 Guest、Reporter、Developer、Maintainer、Owner、Admin、外部用户和项目/组继承权限，验证查看、创建、编辑、合并、运行 pipeline、读取变量和管理安全设置的权限。负向测试非常重要，尤其是 confidential issue、protected branch 和 artifact 访问。

### 33. 如何测试 protected branch？

参考答案：覆盖谁能 push、谁能 merge、是否需要 approval、pipeline 状态、code owner 和强制规则。测试包括直接 push、MR merge、API merge、fork MR 和 admin override。protected branch 是交付安全边界，不能只做 UI 测试。

### 34. 如何测试 Merge Request 流程？

参考答案：覆盖创建、diff、review comment、approval、pipeline、conflict、rebase、squash、merge、close 和 reopen。断言包括状态、权限、通知、审计和目标分支结果。大 diff、二进制文件和大量评论是性能与稳定性重点。

### 35. 如何测试 webhook？

参考答案：覆盖 push、MR、issue、pipeline、job 和 release 等事件，验证 payload、签名/secret、重试、失败、超时、重复事件和顺序。下游系统不可用时应有可诊断日志和重放能力。Webhook 测试要注意敏感字段脱敏。

### 36. 如何测试 audit events？

参考答案：审计应覆盖权限变更、登录、token、变量、项目设置、安全设置、Runner、group 变更和管理员操作。测试要验证谁、何时、从哪里、做了什么和结果。审计日志必须不可篡改、可查询、权限隔离且不泄露 secret。

### 六、性能、可观测性与稳定性

### 37. 如何测试 GitLab Observability？

参考答案：覆盖 traces、metrics、logs、OpenTelemetry、仪表盘、告警和代码变更关联。测试要验证 trace 完整、标签正确、指标准确、日志可查和权限隔离。可观测性应帮助从生产问题追溯到 MR、commit 和 deploy。

### 38. 如何测试 Incident Management？

参考答案：覆盖告警接入、incident 创建、分派、状态流转、on-call、通知、时间线、关联 MR 和事后复盘。测试要验证权限、并发编辑、通知失败和审计。目标是减少 MTTR，并让开发上下文和事件上下文连起来。

### 39. 如何测试大规模 monorepo 性能？

参考答案：构造大文件数、大 diff、大提交历史、多 pipeline 和多 reviewer 场景，测量 clone/fetch、diff、MR 页面、搜索和 pipeline 创建耗时。还要关注 Gitaly、数据库、缓存和前端渲染。大仓性能回归必须有固定基线。

### 40. 如何测试后台队列和异步任务？

参考答案：GitLab 很多功能依赖后台任务，如 pipeline 调度、通知、扫描结果解析和 webhook。测试要覆盖任务入队、执行、失败重试、幂等、超时和队列积压。断言不能只看前端状态，要检查任务日志和最终一致性。

### 41. 如何测试高可用和故障恢复？

参考答案：模拟数据库、Redis、Gitaly、object storage、Runner、外部 registry 和网络故障，验证降级、重试、告警和恢复。关键流程如登录、MR、pipeline 和 artifact 访问应有明确 SLO。故障演练后要补充自动化和 runbook。

### 42. 如何测试升级兼容？

参考答案：覆盖数据库迁移、feature flag、配置兼容、API 兼容、runner 兼容、旧数据读取和回滚。Self-managed 客户升级路径多，测试要覆盖多版本升级和大数据量迁移。对不可逆迁移要有前向修复策略。

### 七、编程、数据与行为面模拟题

### 43. 编程题：如何解析 pipeline DAG 并判断是否存在环？

参考答案：把 job 作为节点，needs 作为有向边，用拓扑排序或 DFS 检测环。如果拓扑排序后处理节点数小于总节点数，说明存在环。面试中要讨论跨 stage、optional needs、child pipeline 和错误提示如何定位到具体 job。

### 44. SQL 题：如何找出过去一天失败率最高的 runner？

参考答案：按 runner_id 聚合过去一天 job 执行记录，统计失败数、总数、失败率、平均排队时间和平均执行时间，并设置最小样本量。再按 executor、tag、项目和错误类型下钻，判断是 runner 环境问题还是代码问题。

### 45. 系统设计题：设计一个 CI/CD 回归测试平台。

参考答案：平台包含 YAML 样例库、项目模板、Runner 池、执行编排、artifact 校验、日志采集、权限矩阵、性能统计和 CI 门禁。每次调度器或 Runner 变更都运行固定 pipeline，比较状态图、耗时、日志、制品和失败原因。平台要支持并发、隔离和资源清理。

### 46. 行为面：生产环境 pipeline 大面积排队，你会如何处理？

参考答案：先确认影响范围、Runner 在线状态、队列长度、调度器错误、最近变更和资源利用率，必要时扩容 Runner 或回滚调度变更。随后分析是否由特定 tag、项目、executor、缓存或外部依赖导致。恢复后补充容量监控、排队告警、压力测试和复盘行动项。

## AI 相关加分点

- 能把 GitLab Duo、AI 代码建议、AI 生成测试、漏洞解释和 Agent Platform 拆成可测指标。
- 熟悉 CI/CD、Runner、pipeline DAG、artifact/cache、protected variables 和发布门禁。
- 能围绕 SAST、DAST、Secret Detection、Dependency Scanning、Container Scanning 和 Code Quality 设计 DevSecOps 回归。
- 能测试 AI 上下文权限、prompt injection、secret 泄露、越权工具调用和 Agent 审计。
- 能用 AI 辅助失败归因、测试生成、MR 摘要和安全修复建议，但保留人工 review 和 CI 验证。
- 能把 pipeline 成功率、排队时间、flaky 率、扫描准确率、AI 采纳率和 P95/P99 纳入质量看板。

## 复习建议

- 重点复习 Git、Merge Request、CI/CD、Runner、artifacts、cache、variables、protected branch 和 webhook。
- 准备一个 CI/CD 自动化测试案例和一个 DevSecOps 安全扫描质量门禁案例。
- 熟悉 GitLab Duo、Agent Platform、AI 代码建议、AI 生成测试和 prompt injection 风险。
- 性能稳定性重点复习大仓库、大 diff、队列、异步任务、Runner 扩缩容和升级迁移。
- 编程题重点练 DAG、拓扑排序、日志解析、SQL 聚合、API client 和权限矩阵。
- 行为面突出开发者体验、快速止损、跨团队协作、数据驱动复盘和质量平台化思维。
