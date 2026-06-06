# AMD 测试开发工程师面试题整理

- 公司：AMD
- 岗位方向：测试开发工程师 / SDET / Software Validation Engineer / GPU Driver QA / AI Platform Quality
- 生成日期：2026-06-07
- 适用场景：EPYC、Ryzen、Radeon、Instinct GPU、ROCm、GPU 驱动、Linux/Windows、数据中心、游戏图形、边缘 AI、Ryzen AI NPU、性能功耗和自动化实验室

## 资料来源与整理依据

- AMD 官方开发者资料：ROCm 文档、ROCm Validation Suite、Ryzen AI Software、AMD AI Hub、Developer Documentation、GPUOpen。
- AMD 产品资料：EPYC、Ryzen、Radeon、Instinct、XDNA NPU、AI PC、数据中心 GPU 和开放 AI 软件生态。
- 公开 AMD validation/SDET 面试方向：Validation Engineer、Software Test Engineer、GPU driver、Linux、C/C++、Python 自动化、计算机体系结构、性能功耗和实验室调试。
- 通用测试开发题型：自动化框架、CI/CD、驱动测试、性能回归、稳定性、日志分析、数据分析、AI 辅助测试和模型部署质量。

> 说明：以下题目不是 AMD 官方题库，而是结合 AMD 产品方向、公开面试经验和测试开发岗位能力模型整理的模拟面试题。

## 面试画像

AMD 的测试开发岗位常见关键词是 CPU/GPU/APU validation、driver、ROCm、Linux/Windows、性能、功耗、温度、硬件矩阵、游戏/图形、AI/HPC workload 和实验室自动化。候选人不仅要会写自动化，还要理解硬件平台、驱动软件栈、日志、benchmark、CI、测试设备和真实客户 workload。AI 方向会关注 ROCm、PyTorch/TensorFlow 兼容、Instinct GPU、Ryzen AI NPU 和模型推理质量。

回答时建议突出：你能把硬件、驱动、runtime、模型、benchmark 和自动化数据串起来，做可复现、可量化、可定位的质量保障。

## 一、岗位理解与质量策略

### 1. 你如何理解 AMD 测试开发工程师的核心价值？

**参考答案：**  
核心价值是保障 CPU、GPU、APU、驱动、ROCm 和 AI 软件栈在多硬件、多系统、多 workload 下稳定可靠。AMD 产品覆盖游戏、PC、服务器、HPC 和 AI，质量不仅是功能通过，还包括性能、功耗、温度、兼容性、长期稳定和客户 workload 表现。测试开发要通过自动化和数据化提升版本准入效率。

### 2. AMD validation 和普通互联网测试有什么不同？

**参考答案：**  
普通互联网测试主要关注页面和 API，AMD validation 还要关注硬件 stepping、BIOS/firmware、驱动、内核、GPU runtime、图形栈、AI 框架、温度和功耗。很多问题表现为性能下降、系统 hang、驱动 reset、GPU kernel 失败或特定硬件组合异常，需要结合日志和指标定位。

### 3. 如何介绍一个 GPU 驱动自动化测试项目？

**参考答案：**  
可以介绍“GPU 驱动回归平台”：自动安装驱动、部署图形和计算 workload、运行 benchmark、采集 dmesg/event log/driver log/perf/功耗温度，比较性能基线并聚类失败。指标包括回归耗时下降、性能回归提前发现、crash 定位时间缩短和自动化稳定性提升。

### 4. 如果加入 AMD，前三个月你会做什么？

**参考答案：**  
先熟悉负责模块，例如 ROCm、Radeon driver、Ryzen AI、Instinct GPU、EPYC 平台或 graphics validation；再梳理自动化覆盖、硬件矩阵、历史缺陷、CI 失败和客户 workload；最后落地专项，如 ROCm 模型兼容评测、GPU 长稳测试、功耗回归或 Ryzen AI NPU 性能评测。

### 5. 如何衡量 AMD 软件质量？

**参考答案：**  
指标包括功能通过率、crash/hang 率、驱动加载成功率、GPU reset 次数、benchmark 性能、功耗、温度、ROCm workload 通过率、AI 模型精度和延迟、框架兼容性、CI flaky 率和客户问题数。核心是把实验室指标和客户真实 workload 关联起来。

## 二、CPU/GPU、驱动与平台测试

### 6. 如何测试 GPU 驱动安装和升级？

**参考答案：**  
覆盖 clean install、upgrade、rollback、卸载、重启、设备识别、版本号、权限和日志。升级后验证图形、计算、视频、多显示器、休眠唤醒和关键 workload。异常场景包括依赖缺失、内核版本不匹配、残留旧驱动和安装中断。

### 7. 如何测试 GPU 计算正确性？

**参考答案：**  
使用固定输入运行 HIP/OpenCL/SYCL 或框架 workload，比较输出和 golden data。覆盖不同数据类型、矩阵尺寸、边界输入、并发 kernel 和长时间运行。要允许合理浮点误差，但不能出现语义级错误。

### 8. 如何测试 GPU 性能回归？

**参考答案：**  
固定硬件、驱动、OS、BIOS、温度和 benchmark，记录吞吐、延迟、显存带宽、PCIe 带宽和功耗。新版本与基线比较，超过阈值自动报警。性能结论必须可复现，避免受环境噪声影响。

### 9. 如何测试 GPU 长时间稳定性？

**参考答案：**  
运行图形、计算、AI、视频和混合 workload 数小时到数天，观察 GPU reset、driver crash、内存泄漏、温度、功耗和性能漂移。长稳测试要保留日志、硬件状态和 workload 时间线，便于定位偶现问题。

### 10. 如何测试 Radeon 游戏图形场景？

**参考答案：**  
覆盖不同 API，如 DirectX、Vulkan、OpenGL；不同分辨率、刷新率、多显示器、全屏/窗口、HDR 和驱动设置。验证画面正确、帧率、卡顿、崩溃、功耗和温度。游戏场景还要覆盖热门游戏和典型引擎。

### 11. 如何测试视频编解码？

**参考答案：**  
覆盖 H.264、HEVC、AV1 等编码格式，不同分辨率、帧率、码率、硬件加速和长时间播放/录制。验证画质、音视频同步、CPU/GPU 占用、功耗和错误恢复。异常包括损坏码流、分辨率切换和并发播放。

### 12. 如何测试多显示器和热插拔？

**参考答案：**  
覆盖 HDMI、DisplayPort、USB-C、不同分辨率、刷新率、缩放、旋转和 HDR。反复插拔、休眠唤醒、切换主屏和关闭显示器，验证显示状态、日志、驱动恢复和用户配置保留。

### 13. 如何测试 CPU 平台特性？

**参考答案：**  
先理解特性规格，如虚拟化、功耗状态、内存控制器、安全扩展或性能计数器，再设计功能、边界、异常和性能用例。验证方式包括微基准、系统日志、BIOS 设置、内核能力和真实 workload。

### 14. 如何定位系统 hang 或 GPU reset？

**参考答案：**  
先确认是系统 hang、驱动超时、GPU reset、kernel panic 还是 workload 卡死。收集 dmesg、Windows event log、crash dump、driver log、温度、功耗和复现步骤。定位要结合最近变更、硬件状态和 workload 时间线。

## 三、ROCm、Instinct GPU 与 AI/HPC 工作负载

### 15. 如何测试 ROCm 安装？

**参考答案：**  
覆盖支持的 Linux 发行版、内核、驱动、GPU 型号、权限、容器和依赖包。安装后验证 `rocminfo`、`rocm-smi`、HIP sample、PyTorch ROCm 和关键库。异常包括内核不匹配、GPU 不可见、权限不足和依赖冲突。

### 16. 如何测试 ROCm Validation Suite？

**参考答案：**  
使用 ROCm Validation Suite 做 GPU 压力、带宽、温度、错误注入和健康检查。测试要记录 GPU 型号、驱动、ROCm 版本、运行参数和错误码。RVS 适合做版本准入和硬件健康检查的一部分。

### 17. 如何测试 PyTorch ROCm 兼容性？

**参考答案：**  
覆盖模型加载、训练、推理、autograd、mixed precision、distributed、常见算子和第三方库。验证结果正确、性能符合基线，并检查是否发生 CPU fallback。还要覆盖不同 PyTorch、ROCm、Python 和驱动版本组合。

### 18. 如何测试 LLM 推理性能？

**参考答案：**  
固定模型、上下文长度、batch size、并发、量化方式和硬件配置，测量 TTFT、tokens/s、P95/P99 延迟、显存、功耗和错误率。要覆盖长上下文、流式输出、多实例和热启动。结果必须记录版本和环境。

### 19. 如何测试分布式训练？

**参考答案：**  
覆盖多 GPU、多节点、通信库、网络带宽、checkpoint、容错和数据并行。验证 loss 曲线、吞吐、GPU 利用率、通信耗时和异常恢复。异常包括节点掉线、显存不足、通信超时和结果不收敛。

### 20. 如何测试 GPU 显存管理？

**参考答案：**  
构造大模型、多进程、频繁分配释放和 OOM 场景，观察显存占用、碎片化、释放及时性和错误提示。测试要验证 OOM 后系统可恢复，不影响后续 workload。显存问题常导致偶现失败和性能抖动。

### 21. 如何测试 HIP kernel？

**参考答案：**  
对 kernel 做功能、边界、数据类型、线程块配置、共享内存、同步和错误输入测试。输出与 CPU reference 对比，使用工具检查非法访问和 race。性能测试还要关注 occupancy、内存访问和 kernel fusion。

### 22. 如何测试容器化 ROCm workload？

**参考答案：**  
覆盖 Docker/Podman/Kubernetes 环境中的 GPU passthrough、权限、驱动挂载、镜像版本和设备可见性。验证容器内 `rocminfo`、框架 workload 和多容器隔离。异常包括驱动/runtime 版本不匹配和资源泄漏。

### 23. 如何测试 AI benchmark 的可信度？

**参考答案：**  
固定模型、数据集、batch、精度、warmup、采样次数和环境变量，避免 cherry-pick。报告平均值、P95、方差、功耗和显存。benchmark 要能复现，并说明是否包含预处理、后处理和数据加载时间。

### 24. 如何测试框架升级兼容性？

**参考答案：**  
准备旧版本脚本、模型、容器和真实 workload，升级 PyTorch/TensorFlow/ROCm 后验证功能、精度、性能和错误提示。升级失败要能回滚。重点关注 API 变化、算子实现、精度漂移和依赖冲突。

## 四、Ryzen AI、边缘 AI 与端侧推理

### 25. 如何测试 Ryzen AI NPU 应用？

**参考答案：**  
覆盖模型转换、量化、NPU 后端选择、输入输出、性能、功耗、温度和错误处理。验证应用确实运行在 NPU 上，而不是 silent fallback 到 CPU/iGPU。还要测试不同 Windows 版本、驱动和 Ryzen AI SDK 版本。

### 26. 如何测试模型量化精度？

**参考答案：**  
使用固定评测集比较原始模型、量化模型和端侧运行结果。指标根据任务选择 accuracy、mAP、WER、BLEU 或人工评分。允许合理误差，但必须有阈值和失败样本分析。

### 27. 如何测试端侧 AI 功耗？

**参考答案：**  
使用功耗仪或平台工具测量单次推理、连续推理、多模型并发和后台推理。记录后端、模型版本、输入大小、温度、频率和电池状态。端侧 AI 要平衡精度、延迟和功耗。

### 28. 如何测试多后端一致性？

**参考答案：**  
同一模型分别在 CPU、iGPU、NPU 或离散 GPU 上运行，比较输出、延迟、内存和功耗。允许浮点误差，但不能出现明显语义差异。后端选择和 fallback 状态必须可观测。

### 29. 如何测试 AI 隐私安全？

**参考答案：**  
验证输入数据是否本地处理、日志是否泄露图片/语音/文本、模型缓存是否加密、权限是否最小化。构造敏感输入和越权访问场景，确认不会把个人数据上传或写入未脱敏日志。

### 30. 如何测试 AI 开发工具？

**参考答案：**  
覆盖安装、模型导入、分析、profiling、可视化、错误提示和导出。验证工具输出与真实运行一致，能帮助定位性能瓶颈。异常包括 unsupported op、动态 shape、错误模型和版本不兼容。

## 五、自动化、CI/CD、性能功耗与实验室

### 31. 如何设计 AMD 场景自动化框架？

**参考答案：**  
框架应支持设备管理、驱动安装、workload 调度、benchmark 执行、日志采集、功耗温度采集、结果对比和失败聚类。可以使用 Python、pytest、Bash、PowerShell、ROCm 工具、系统 API 和实验室设备 API。框架要支持硬件矩阵和并发隔离。

### 32. 如何管理测试硬件池？

**参考答案：**  
记录设备型号、GPU/CPU、BIOS、驱动、OS、ROCm、占用状态、健康检查和位置。CI 按需求分配设备，测试后自动恢复基线。硬件池要有故障隔离和资源利用率看板。

### 33. 如何治理 flaky 自动化？

**参考答案：**  
先区分硬件状态、环境温度、驱动状态、设备占用、等待策略、真实缺陷和脚本问题。治理方式包括健康检查、环境重置、显式状态轮询、失败聚类、owner 机制和稳定性阈值。硬件测试中 flaky 可能是稳定性问题的信号。

### 34. 如何做功耗测试？

**参考答案：**  
固定环境温度、驱动、BIOS、workload 和系统设置，使用功耗仪或平台工具测量 idle、游戏、AI 推理、训练、视频和高负载。功耗结果要和性能一起分析，避免只追求性能而牺牲能效。

### 35. 如何测试温度和降频？

**参考答案：**  
构造持续高负载，监控温度、频率、功耗、性能、风扇和 throttling。验证热保护策略有效，且性能下降符合预期。测试必须记录环境温度和机箱/散热条件。

### 36. 如何设置 CI/CD 质量门禁？

**参考答案：**  
门禁包括编译、单元测试、驱动安装冒烟、GPU/CPU workload、ROCm sample、关键 AI 模型、性能基线、功耗基线、crash/hang 阈值和 flaky 阈值。高风险变更还要增加长稳和硬件矩阵测试。

### 37. 如何设计质量看板？

**参考答案：**  
看板应包含版本、硬件、OS、驱动、ROCm、用例、失败原因、crash signature、性能趋势、功耗趋势、温度趋势和设备健康。支持按平台、模块、提交和 workload 下钻。AI 可以辅助摘要，但原始日志和指标必须保留。

### 38. 如何测试客户 workload？

**参考答案：**  
选择真实代表性场景，如游戏、视频转码、LLM 推理、分布式训练、HPC kernel、数据库和编译。固定数据集、参数、版本和环境，记录功能、性能、功耗和稳定性。客户 workload 比单一 micro benchmark 更接近真实质量。

## 六、编码、SQL 与 Linux

### 39. 编程题：如何判断系统大小端？

**参考答案：**  
定义整数 `0x0102`，读取低地址字节。如果低地址是 `0x02`，说明是小端；如果是 `0x01`，说明是大端。大小端在硬件寄存器、驱动和二进制协议中很常见。

### 40. 编程题：如何统计二进制中 1 的个数？

**参考答案：**  
使用 `n = n & (n - 1)` 每次消掉最低位的 1，循环计数直到 n 为 0。时间复杂度与 1 的个数相关。要说明无符号数、负数和位宽处理方式。

### 41. 编程题：如何实现简单 LRU Cache？

**参考答案：**  
使用哈希表加双向链表。哈希表 O(1) 查找节点，双向链表维护访问顺序，访问或更新时移动到头部，容量超限时删除尾部。测试要覆盖更新已有 key、容量为 0、并发访问和删除顺序。

### 42. SQL：如何统计每个平台最近 7 天 GPU reset 率？

**参考答案：**  
按平台、日期、版本聚合 reset 设备数和活跃设备数，reset 率等于 reset_device_count / active_device_count。实际要去重同一设备多次 reset，并按硬件型号、驱动版本和 workload 切片。

### 43. Linux：如何排查 GPU 设备不可见？

**参考答案：**  
先看 `lspci` 是否能看到设备，再检查驱动模块、dmesg、权限、IOMMU、内核版本和容器设备映射。ROCm 场景下还要看 `rocminfo`、用户组权限和 runtime 版本。要区分硬件枚举、驱动加载和用户态 runtime 问题。

### 44. Linux：如何排查进程内存泄漏？

**参考答案：**  
使用 `top`、`pmap`、`smem`、`/proc/<pid>/smaps` 观察趋势，结合 valgrind、asan、heap profiler 或应用日志定位。GPU/AI 场景还要同时观察显存泄漏和 host memory 泄漏。

### 45. Linux：如何排查 CPU/GPU 性能异常？

**参考答案：**  
先确认 workload、版本和环境，再查看频率、温度、功耗、CPU/GPU 利用率、内存带宽、PCIe 带宽和日志。使用 perf、benchmark、rocm-smi 或平台工具定位瓶颈。性能异常要和基线比较，而不是凭感觉判断。

### 46. 如何写一个稳定的自动化用例？

**参考答案：**  
稳定用例应有独立数据、明确前置条件、显式等待、可靠清理、清晰断言和失败日志。硬件/驱动测试还要记录设备状态、版本、温度和 workload 参数。用例失败时应能帮助定位，而不是只告诉“失败”。

## AI 相关加分点

- 能把 ROCm/Instinct AI 测试拆成安装、框架兼容、算子、模型精度、性能、显存、分布式和容器部署。
- 能把 Ryzen AI 测试拆成模型转换、NPU 后端、量化精度、功耗、温度、多后端一致性和隐私。
- 能说明 silent fallback、unsupported op、精度漂移、性能回归、显存泄漏和版本兼容风险。
- 能用 AI 做日志摘要、失败聚类和测试生成，但知道驱动、性能、功耗和模型正确性必须由确定性指标验证。
- 能围绕客户 workload 建立可复现 benchmark，而不是只跑 demo。

## 复习建议

- 重点复习 C/C++、位运算、大小端、Linux、GPU 基础、驱动、性能分析、Python 自动化和 CI/CD。
- 准备一个“GPU/ROCm 自动化测试平台”项目故事，说明硬件池、驱动安装、workload 执行、日志采集和性能对比。
- 熟悉 ROCm、HIP、PyTorch ROCm、Instinct GPU、Ryzen AI、NPU、模型量化和推理性能指标。
- 多练习从功能、兼容性、性能、功耗、温度、稳定性、安全和客户 workload 多角度回答。
- 行为面试中突出跨硬件、驱动、AI 软件、测试和客户团队协作定位复杂问题的能力。
