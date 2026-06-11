# Replicate 测试开发工程师面试题

## 公司名

Replicate

## 岗位方向

测试开发工程师 / SDET / 质量工程方向，重点面向 AI 模型推理平台、Predictions API、异步任务、Streaming、Webhooks、模型部署、文件输入输出、Rate Limits、数据保留、安全检查、成本治理、可观测性、CI/CD 与 AI 辅助测试平台。

## 资料来源与整理依据

- [Replicate Docs](https://replicate.com/docs)
- [HTTP API Reference](https://replicate.com/docs/reference/http)
- [Run a model](https://replicate.com/docs/topics/models/run-a-model)
- [Predictions](https://replicate.com/docs/topics/predictions)
- [Create a prediction](https://replicate.com/docs/topics/predictions/create-a-prediction)
- [Input files](https://replicate.com/docs/topics/predictions/input-files)
- [Output files](https://replicate.com/docs/topics/predictions/output-files)
- [Prediction lifecycle](https://replicate.com/docs/topics/predictions/lifecycle)
- [Streaming](https://replicate.com/docs/topics/predictions/streaming)
- [Rate limits](https://replicate.com/docs/topics/predictions/rate-limits)
- [Safety checking](https://replicate.com/docs/topics/predictions/safety-checking)
- [Data retention](https://replicate.com/docs/topics/predictions/data-retention)
- [Webhooks](https://replicate.com/docs/topics/webhooks)
- [Verify webhooks](https://replicate.com/docs/topics/webhooks/verify-webhook)
- [Deployments](https://replicate.com/docs/topics/deployments)
- [Create a deployment](https://replicate.com/docs/topics/deployments/create-a-deployment)

## 面试画像

Replicate 的测试开发岗位会更关注“模型平台工程质量”：不仅要测 HTTP API、鉴权、SDK、文件上传、异步任务、Webhook、部署和限流，还要理解不同模型的输入输出 schema、GPU 推理延迟、模型版本、冷启动、输出文件保留、安全检查和成本。回答时建议围绕“预测任务生命周期 -> 模型/部署版本 -> 文件与结果可靠性 -> 性能成本 -> 安全合规 -> 线上可观测”展开。

## 题目分类

- 岗位理解与 AI 模型平台质量体系
- Predictions API、模型运行与任务生命周期
- 文件输入输出、Streaming 与 Webhooks
- Deployments、模型版本与发布质量
- 性能稳定性、限流、成本与可观测性
- 安全检查、数据保留与合规治理
- CI/CD、测试平台与 AI 辅助测试
- 编程、数据与行为面模拟题

## 一、岗位理解与 AI 模型平台质量体系

### 1. 你如何理解 Replicate 测试开发工程师和普通后端测试开发的差异？

参考答案：普通后端测试更关注接口契约、数据库一致性、并发和异常处理；Replicate 这类 AI 推理平台还要关注模型输入输出 schema、异步 prediction 生命周期、GPU 冷启动、模型版本、部署扩缩容、文件上传下载、Webhook 可靠性、流式输出、输出文件保留、安全检查和成本。测试开发不能只判断接口是否 200，还要建立任务成功率、排队耗时、推理耗时、输出可用率、Webhook 到达率、模型版本退化、限流命中和单位预测成本等指标。

### 2. 如果让你负责 Replicate API 的端到端质量，你会如何分层？

参考答案：我会分六层：第一层是 API 契约，覆盖鉴权、请求字段、错误码、SDK 和模型 schema；第二层是 prediction 生命周期，覆盖 starting、processing、succeeded、failed、canceled 等状态流转；第三层是文件和结果，覆盖 input files、output files、URL 可用性、二进制格式和数据保留；第四层是部署质量，覆盖模型版本、deployments、扩缩容、冷启动和灰度；第五层是非功能，覆盖限流、延迟、吞吐、重试、成本和稳定性；第六层是安全合规，覆盖安全检查、secrets、日志脱敏和数据删除。

### 3. AI 模型平台的“正确性”如何定义？

参考答案：正确性包括两类。平台正确性是请求被正确鉴权、调度、执行、状态更新、结果保存和回调；模型正确性是模型输出符合输入 schema 和业务预期，例如图片、音频、文本或 JSON 是否可解析且质量达标。测试时要把模型能力指标和平台 SLA 分开，避免模型效果波动掩盖平台故障，也避免平台错误被误判为模型退化。

### 4. 如何设计 Replicate 的核心质量指标？

参考答案：核心指标包括 prediction 创建成功率、状态流转成功率、任务排队时长、推理时长、P95/P99 总耗时、失败率、取消成功率、输出文件可下载率、Webhook 到达率、Webhook 验签成功率、限流命中率、模型冷启动时长、部署健康、GPU 利用率、成本和安全拦截率。指标要按模型、版本、deployment、客户、输入类型和地区切分。

### 5. 如果用户反馈“模型调用偶尔失败”，你会如何定位？

参考答案：先拿 request id 或 prediction id，查看请求参数、模型版本、输入文件、状态流转、错误信息、队列耗时、推理日志和输出文件。再按模型、deployment、时间段、客户、输入大小和硬件类型聚合，判断是单个模型问题、调度问题、文件问题、限流、资源不足还是安全检查失败。最后构造可复现用例加入回归集，并补充监控或错误信息。

### 6. 模型平台为什么特别需要灰度和回滚能力？

参考答案：模型升级可能改变输出质量、schema、耗时和资源消耗，部署配置变更可能影响冷启动、扩缩容和成本。灰度能让新模型或新部署先承接少量流量，并用任务成功率、质量评测、延迟和成本对比旧版本。回滚要能快速切回旧版本或旧 deployment，同时保证正在运行的 prediction 状态和输出文件不丢失。

## 二、Predictions API、模型运行与任务生命周期

### 7. 如何测试 Create Prediction API 的基础契约？

参考答案：覆盖 version、deployment、input、webhook、stream、wait、鉴权、非法模型、非法版本、缺少必填字段、输入类型错误、超大输入和余额/权限不足。断言 HTTP 状态码、错误结构、prediction id、status、urls、created_at、input、output、error、logs 和 metrics 等字段。还要测试 SDK 调用和原始 HTTP 调用的一致性。

### 8. Prediction 生命周期有哪些测试点？

参考答案：测试从创建到 queued/starting/processing/succeeded/failed/canceled 的状态流转是否符合预期。用例包括成功任务、模型报错、输入文件下载失败、用户取消、超时、资源不足和安全检查失败。断言状态不可逆、错误信息可诊断、输出只在成功后可用、取消后不会继续扣费或产生新输出。

### 9. 同步等待和异步轮询有什么测试差异？

参考答案：同步等待要测试 wait 参数、超时边界、长任务返回 pending、短任务直接返回结果和客户端超时；异步轮询要测试状态查询频率、最终一致性、重复查询、任务过期和错误处理。业务上应避免长任务阻塞 HTTP 连接，也要防止客户端高频轮询造成额外压力。自动化要覆盖两种模式的结果一致性。

### 10. 如何测试模型输入 schema？

参考答案：每个模型都有不同 input schema，要自动拉取或维护 schema，生成必填、可选、默认值、类型错误、边界值、枚举值和文件输入用例。断言服务端对非法输入返回明确错误，不会进入 GPU 推理才失败。对 schema 变化要做兼容性测试，避免新版本删除字段或改变默认值导致客户调用失败。

### 11. 如何验证模型输出 schema？

参考答案：根据模型类型验证输出：文本要检查字符串、JSON 或流式片段；图片/音频/视频要检查 URL、文件格式、可下载、可解码、尺寸/时长；结构化结果要做 JSON Schema 校验。还要覆盖失败输出、空输出、部分输出、多个输出文件和输出文件过期。输出 schema 应随模型版本记录，避免客户端解析被破坏。

### 12. 如何测试 prediction 取消功能？

参考答案：构造 queued、starting、processing 三种阶段的取消请求，验证状态最终变为 canceled 或已完成不可取消。断言取消后不会继续执行、不会产生新的输出文件、不会重复回调成功事件，并且成本和日志符合策略。并发场景要测试重复取消和取消与完成同时发生的竞态。

### 13. 如何测试模型运行的可复现性？

参考答案：如果模型支持 seed 或 deterministic 参数，就固定 version、input、seed、硬件和参数，多次运行比较输出 hash、相似度或结构化结果；如果模型本身有随机性，就定义统计范围。还要区分平台可复现和模型可复现：同一 version 的平台行为要稳定，模型输出可以有合理波动但不能破坏业务契约。

### 14. 如何处理不同模型运行时间差异很大的测试？

参考答案：测试集要按模型耗时分层，CI 只跑快速 smoke，夜间跑长耗时模型，发布前跑核心模型回归。超时阈值不能一刀切，要按模型和输入大小定义。测试平台要支持异步调度、并发控制、断点续跑和成本预算，避免长任务阻塞整个流水线。

## 三、文件输入输出、Streaming 与 Webhooks

### 15. Input files 的测试重点是什么？

参考答案：覆盖本地文件上传、远程 URL、不同格式、超大文件、空文件、损坏文件、文件名特殊字符、Content-Type 错误和访问受限 URL。断言文件被正确下载、校验、传给模型，并在失败时返回可诊断错误。安全上要测试 SSRF、防路径穿越、压缩炸弹、恶意元数据和私有网络 URL。

### 16. Output files 的测试重点是什么？

参考答案：验证输出 URL 可访问、文件格式正确、大小合理、可解码、过期策略符合文档、多个输出顺序正确。还要测试下载中断、重复下载、结果过期、权限隔离和对象存储异常。业务客户端应及时保存需要长期使用的结果，测试要覆盖过期后访问的错误处理。

### 17. 如何测试 Streaming 输出？

参考答案：覆盖开启 stream、模型支持流式、模型不支持流式、SSE chunk 顺序、增量拼接、连接中断、慢消费者、服务端错误和最终完成事件。断言每个 chunk 可解析、不会重复或丢失、错误能传播、最终结果和非流式结果语义一致。还要单独采集首 chunk 延迟和完整响应延迟。

### 18. Webhooks 的测试重点是什么？

参考答案：覆盖 webhook URL 配置、事件类型、成功回调、失败回调、重试、超时、重复投递、乱序、目标服务 500、网络不可达和事件签名。断言 payload 包含 prediction id、status、output、error 等必要信息，且业务方能够幂等处理。测试还要模拟接收端慢响应和短暂故障。

### 19. 如何验证 Webhook 签名？

参考答案：根据官方验签机制，接收端要用共享密钥或签名头验证请求来源。测试包括正确签名、错误签名、缺失签名、旧时间戳、重复请求、payload 被篡改和密钥轮换。断言未通过验签的 webhook 不会被业务处理，并记录安全日志。还要注意原始请求体不能在验签前被 JSON 格式化破坏。

### 20. 如何处理 Webhook 重复投递？

参考答案：Webhook 通常应按至少一次投递设计，业务方必须幂等。测试要用相同 prediction id 和事件 id 重复投递，验证不会重复写库、重复通知或重复扣费。可以用事件去重表、状态机和乐观锁控制。乱序投递时，业务状态只能向前推进，不能从 succeeded 回退到 processing。

### 21. 如何测试文件与 Webhook 联动场景？

参考答案：构造长任务完成后通过 webhook 通知业务下载 output files 的场景。测试包括 webhook 到达时文件可下载、文件暂时不可用后重试、文件过期、下载失败和重复 webhook。业务方应把下载结果和 prediction 状态绑定，记录重试次数，避免 webhook 成功但文件未保存。

### 22. 如何测试 share prediction 或公开结果相关能力？

参考答案：要验证公开链接的权限、脱敏、过期、撤销、输入输出展示和隐私边界。用例包括公开成功、私有 prediction 不可见、跨账号访问、删除后访问、敏感输入不展示。公开分享类能力要特别关注是否泄露原始输入文件、secrets、日志或内部错误。

## 四、Deployments、模型版本与发布质量

### 23. Deployments 和直接调用模型版本有什么区别？

参考答案：直接调用模型版本适合固定 version 运行，deployment 则更像生产服务入口，可以绑定模型版本、硬件和配置，便于升级、监控和扩缩容。测试 deployment 时要关注路由、版本切换、冷启动、健康检查、权限和监控；直接调用 version 时更关注版本不可变性和 schema 稳定性。

### 24. 如何测试创建 Deployment？

参考答案：覆盖模型、版本、硬件、最小/最大实例、权限、名称冲突、非法配置和配额不足。断言 deployment 状态、可调用性、配置持久化、监控指标和错误信息。创建后要跑 smoke prediction，确认实际路由到目标版本和硬件，并能在日志中追踪。

### 25. 如何测试 Deployment 更新和回滚？

参考答案：先用旧版本建立基线，再更新到新版本，跑兼容性、延迟、成功率和输出质量对比。回滚时验证新请求回到旧版本，正在运行的任务不丢失，指标和日志能区分版本。还要测试配置更新失败、部分生效、并发更新和权限不足。回滚流程必须自动化演练。

### 26. 如何测试 Deployment 冷启动和扩缩容？

参考答案：构造长时间无流量后的首次请求，记录冷启动时间；再逐步增加并发，观察实例扩容、排队、延迟和失败率。缩容测试要看空闲后资源是否释放，下一次请求是否可用。指标包括 cold start P95、扩容耗时、队列长度、GPU 利用率和成本。

### 27. 如何测试私有模型或自定义模型部署？

参考答案：覆盖镜像构建、依赖安装、模型加载、predict 函数输入输出、GPU 兼容、secrets、日志、错误处理和资源限制。测试样本包括正常输入、非法输入、大文件和超时任务。还要验证私有模型只能被授权账号调用，日志不会泄露权重路径、token 或 secrets。

### 28. 如何设计模型版本兼容性测试？

参考答案：维护不同版本的输入输出 schema、默认参数、资源需求和质量基线。升级时比较 schema 变化、输出类型、失败率、延迟、成本和代表性样本质量。对破坏性变更要有明确版本号和迁移指南，测试要验证旧客户端仍可调用旧版本。

## 五、性能稳定性、限流、成本与可观测性

### 29. 如何设计 Prediction API 的性能压测？

参考答案：按模型类型、输入大小、输出类型、同步/异步、streaming、webhook 和 deployment 建立压测矩阵。指标包括 prediction 创建 QPS、排队耗时、推理耗时、P95/P99 总耗时、失败率、429 比例、Webhook 延迟、输出下载成功率、GPU 利用率和单位任务成本。压测要区分轻量模型和重型 GPU 模型。

### 30. 如何测试 Rate Limits？

参考答案：构造超过请求速率、并发、输入大小或账号配额的请求，验证是否返回明确错误和可重试信息。客户端要测试指数退避、随机抖动、队列控制和最大重试次数。还要验证不同 API token、账号、模型和 deployment 的隔离，避免一个调用方影响其他调用方。

### 31. 如何做成本治理测试？

参考答案：按模型、硬件、运行时间、输入输出文件、重试、失败、取消和 deployment 实例统计成本。测试要对比平台用量、账单、日志和业务侧埋点。异常场景包括客户端超时但任务继续运行、Webhook 重复导致重复处理、取消失败、长任务超时和输出文件重复下载。

### 32. 如何设计线上监控和告警？

参考答案：监控包括 API 可用性、prediction 创建失败率、状态失败率、排队时长、推理时长、P99 延迟、限流、Webhook 失败率、输出文件下载失败、deployment 健康、冷启动、GPU 资源和成本异常。告警应按模型、version、deployment、客户和地区切分，并提供 prediction id 链接方便回放。

### 33. 如果 P99 总耗时升高，你会如何定位？

参考答案：先拆分总耗时：API 创建、队列等待、模型启动、推理执行、输出上传、Webhook 回调和客户端下载。再按模型、deployment、输入大小、硬件、客户和时间段切分。若排队增加，查资源和限流；若推理增加，查模型版本和输入；若输出增加，查对象存储和网络。

### 34. 稳定性浸泡测试如何设计？

参考答案：用生产相似的混合流量持续运行，覆盖短文本模型、图像模型、视频模型、文件输入、streaming、webhook、deployment 和异常请求。监控内存、文件句柄、队列长度、GPU 利用率、对象存储、日志量、失败率、延迟和成本。重点发现资源泄漏、队列堆积、输出文件清理异常和长尾任务积压。

## 六、安全检查、数据保留与合规治理

### 35. 如何测试 API token 和权限安全？

参考答案：覆盖无 token、错误 token、过期 token、权限不足、跨账号 prediction、私有模型访问、deployment 权限和日志脱敏。测试要检查错误信息、日志、Webhook payload 和公开分享链接中是否泄露 token、secrets 或内部路径。token 轮换后旧 token 应按策略失效。

### 36. Safety checking 的测试重点是什么？

参考答案：要覆盖文本 prompt、输入文件、输出结果和多模态组合的安全策略。样本包括暴力、成人、仇恨、违法、隐私、名人肖像、深伪、版权和正常敏感讨论。指标同时看漏拦率和误拦率，避免安全策略过严影响正常使用。测试还要验证被拦截时状态、错误信息和成本策略。

### 37. Data retention 如何测试？

参考答案：根据官方数据保留策略，测试 prediction、input files、output files、logs 和公开分享结果的保留、过期、删除和不可访问行为。用例包括结果生成后立即访问、接近过期访问、过期后访问、用户删除、账号隔离和审计。业务方应及时保存需要长期保留的输出，测试要验证过期后的客户端提示。

### 38. Secrets 管理有哪些测试点？

参考答案：私有模型或部署可能需要 secrets。测试要验证 secrets 只能在运行环境读取，不能出现在日志、错误、Webhook、输出文件或公开页面中。用例包括缺失 secret、错误 secret、secret 轮换、权限不足和模型异常打印环境变量。安全扫描要把 secrets 泄露作为阻断项。

### 39. 如何防止恶意输入文件攻击？

参考答案：测试 SSRF、私有网络 URL、超大文件、压缩炸弹、损坏图片、恶意 EXIF、路径穿越、伪装 Content-Type 和脚本文件。服务端要做文件类型校验、大小限制、下载隔离、超时和元数据清理。错误应可诊断但不能泄露内部网络、存储路径或凭据。

### 40. Webhook 安全如何保证？

参考答案：Webhook 接收端要验签、检查时间戳、防重放、限制来源、幂等处理和记录审计。测试包括伪造签名、过期时间戳、payload 篡改、重复事件、乱序事件和大 payload。未通过安全校验的 webhook 不能改变业务状态。

## 七、CI/CD、测试平台与 AI 辅助测试

### 41. 如何把 Replicate 模型调用测试接入 CI/CD？

参考答案：PR 阶段跑轻量 smoke，覆盖鉴权、schema、短任务、输出文件和错误码；夜间跑长任务、streaming、webhook、deployment 和质量评测；发布前跑新旧版本对比和灰度检查。CI 要有成本预算和超时控制，避免昂贵模型在每次提交都全量运行。

### 42. 如何设计模型平台自动评测系统？

参考答案：系统包括样本库、模型/版本/部署配置、任务调度、结果采集、输出解析、质量评分、人工复核、报告和失败样本回放。支持文本、图片、音频、视频和 JSON 输出。报告要展示成功率、延迟、成本、质量分、错误分类和版本趋势，并能一键创建回归用例。

### 43. AI 辅助测试可以怎样落地？

参考答案：可以用 LLM 生成模型输入边界、prompt 变体、Webhook 测试 payload、错误日志摘要和失败样本聚类；用视觉/音频模型初筛生成结果质量。但关键断言仍要用 schema、文件解析、状态机、统计指标和人工抽检兜底。AI 辅助测试的价值是扩大覆盖和提升分析效率。

### 44. 模型平台测试中的 flaky 如何治理？

参考答案：先区分模型随机性、GPU 资源波动、队列波动、Webhook 网络抖动、评分器不稳定和外部文件 URL 变化。对模型随机性固定 seed 或做统计判断；对性能波动增加样本量和隔离环境；对 Webhook 做幂等和重试；对评分器做人工校准。flaky 要分类记录，不能简单重跑掩盖风险。

## 八、编程、数据与行为面模拟题

### 45. 编程题：如何实现一个 Prediction 状态轮询客户端？

参考答案：客户端创建 prediction 后按退避策略轮询状态，直到 succeeded、failed 或 canceled。需要设置总超时、最大轮询间隔、429 退避、网络异常重试和取消逻辑。成功时下载并校验 output files，失败时记录 error、logs 和 prediction id。测试覆盖立即成功、长时间 processing、失败、取消、429、网络中断和输出过期。

### 46. 行为面：研发认为“模型输出波动不可测”，你会如何推动？

参考答案：我会先承认模型输出有随机性，然后把风险拆成平台稳定性和模型质量两部分。平台稳定性用状态机、schema、文件、Webhook 和延迟做确定性断言；模型质量用固定样本、seed、统计阈值、人工抽检和模型裁判做趋势评估。先用小范围高价值样本证明评测能发现真实退化，再逐步扩展自动化平台和发布门禁。

## AI 相关加分点

- 能把模型平台质量拆成 API 契约、prediction 生命周期、输出文件、Webhook、部署健康、限流、成本和安全检查。
- 熟悉异步任务、轮询、SSE Streaming、Webhook 验签、重复投递、输出文件过期和幂等处理。
- 能设计多模型、多版本、多硬件、多 deployment 的评测矩阵。
- 会用 schema 校验、文件解析、图像/音频质量评估、模型裁判和人工复核组合做 AI 输出评测。
- 对性能成本敏感：GPU 冷启动、队列等待、推理耗时、P99、取消、重试和单位 prediction 成本。
- 对安全合规有意识：API token、secrets、恶意文件、数据保留、安全检查、公开分享和 Webhook 防重放。

## 复习建议

1. 熟悉 Replicate 的 Predictions、Create Prediction、Streaming、Webhooks、Deployments、Rate Limits 和 Data Retention 文档。
2. 准备一个异步任务测试案例，讲清状态机、轮询、Webhook、输出文件、超时和幂等。
3. 复习 HTTP API、multipart/URL 文件输入、对象存储、SSE、Webhook 签名、限流退避和成本统计。
4. 准备模型平台性能测试思路：排队、冷启动、推理耗时、输出上传、P99 和 GPU 资源。
5. 对安全题要能讲 API token、secrets、恶意文件、SSRF、公开分享和数据保留。
6. 面试回答尽量体现“平台确定性断言 + 模型质量统计评估 + 线上回放闭环”。
