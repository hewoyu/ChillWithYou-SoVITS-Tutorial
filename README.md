# ChillWithYou-SoVITS-Tutorial
针对《Chill With You》AI 对话 Mod 原生语音还原度不足的问题，提供 GPT-SoVITS-v2pro 角色语音克隆全流程教程，完整覆盖资源解包、数据集制作、分阶段训练、Mod API 对接全步骤，个人非商用学习用途

# Chill With You 游戏AI语音定制训练全流程教程
本项目为《Chill With You》游戏AI全语音对话Mod（官方仓库：https://github.com/qzrs777/AIChat/tree/main ）的配套定制训练教程，针对原Mod默认直接调用游戏原生语音、自由对话场景下音色还原度不足、语气生硬的问题，提供基于 **GPT-SoVITS-v2pro-20250604** 的角色语音克隆全流程操作指南，本教程全程操作参考B站UP主对应教程，仅用于个人学习研究。

> 注：本次教程中引用了[《GPT-SoVITS指南》](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e?# 《GPT-SoVITS指南》)文档

---

## 目录
- [免责声明](#免责声明)
- [核心参考资料](#核心参考资料)
- [硬件与环境要求](#硬件与环境要求)
- [全流程操作步骤](#全流程操作步骤)
- [ASR语音识别标注终端运行说明](#asr语音识别标注终端运行说明)
- [常见问题与避坑指南](#常见问题与避坑指南)
- [开源协议](#开源协议)

---

## 免责声明
1.  本教程仅用于**个人非商用的学习研究用途**，严禁将本教程内容、训练后的模型、提取的游戏资源用于商用、二次传播、侵权等违规行为。
2.  《Chill With You》游戏版权归原游戏厂商所有，本教程仅提供操作方法，不提供任何游戏本体、解包资源、原生语音素材，使用本教程提取游戏资源需遵守相关法律法规与游戏用户协议。
3.  本教程引用的所有教程、工具、模型、Mod的版权均归原作者所有，所有操作均为原教程的场景化适配，不涉及原内容的二次分发与修改。
4.  使用本教程产生的任何法律责任、侵权风险，均由使用者自行承担，本项目作者不承担任何相关责任。

---

## 核心参考资料
本教程所有操作均基于以下官方/原作者教程与工具，聪音角色语音的GPT-SoVITS-v2pro训练全程参考对应UP主的教程，如需学习完整操作，可直接访问对应教程链接：
| 内容类型 | 来源地址 | 用途说明 |
| --- | --- | --- |
| 游戏AI Mod官方仓库 | [qzrs777/AIChat](https://github.com/qzrs777/AIChat/tree/main) | 《Chill With You》AI全语音对话Mod本体下载、安装、配置官方说明 |
| GPT-SoVITS-v2pro核心训练教程 | [B站BV1GJ4m1e7x2](https://www.bilibili.com/video/BV1GJ4m1e7x2/?spm_id_from=333.1391.0.0&vd_source=902071e41a8b164e8f691001d9949343) | 本教程核心训练操作标准，聪音角色语音克隆全程参考该UP主教程 |
| GPT-SoVITS-v2pro下载与部署教程 | [语雀《GPT-SoVITS指南》](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e?#) | 提供GPT-SoVITS-v2pro的完整下载教程、官方下载链接与环境部署指南 |
| 游戏解包教程 | [B站BV1NVwYecESx](https://www.bilibili.com/video/BV1NVwYecESx/?spm_id_from=333.1391.0.0) | Unity游戏资源解包、语音素材提取操作标准 |
| 解包工具官方地址 | [C++重构版AssetStudio](https://www.icloud.com.cn/iclouddrive/0cbLOMljXohDHb1L1D1QIZPcQ#Release) | 游戏资源解包专用工具，适配Unity 2022版本 |
| 解包工具优化说明 | [B站BV1CNZdBzEfR](https://www.bilibili.com/video/BV1CNZdBzEfR/?spm_id_from=333.1391.0.0) | 重构版AssetStudio工具使用说明 |
| 游戏AI Mod演示教程 | [B站BV1x3mnBpE9E](https://www.bilibili.com/video/BV1x3mnBpE9E/?spm_id_from=333.337.search-card.all.click) | Mod安装、API对接演示教程 |
| GPT-SoVITS官方教程 | 项目原作者花儿不哭B站官方账号 | v2pro版本权威功能与参数说明 |

---

## 硬件与环境要求
| 项目 | 最低要求 | 推荐配置 |
| --- | --- | --- |
| 显卡 | NVIDIA显卡，显存≥4G | NVIDIA显卡，显存≥6G |
| 系统 | Windows 10 及以上 | Windows 10/11 64位 |
| 训练环境 | GPT-SoVITS-v2pro-20250604 一键整合包 | 同左，无需额外人声分离工具 |
| 解包工具 | C++重构版AssetStudio | 同左 |

---

## 全流程操作步骤
### 1. 前置工具与环境准备
1.  下载并安装C++重构版AssetStudio，工具操作可参考对应解包教程与官方说明。
2.  参考语雀《GPT-SoVITS指南》（https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e?#）的下载与部署教程，获取并部署GPT-SoVITS-v2pro-20250604整合包，全程操作可对应B站核心训练教程。
3.  因解包获取的聪音语音为无伴奏纯净人声干声，无需额外使用UVR5人声分离工具进行处理。

### 2. 游戏角色语音素材解包与初筛
1.  打开重构版AssetStudio，通过`File→Load file/Load folder`加载《Chill With You》游戏资源目录，操作完全对应解包教程步骤。
2.  切换至`Asset List`标签页，筛选`Type=AudioClip`类型的资源，定位并导出游戏核心角色聪音的全部原生人声台词。
3.  素材初筛：经解包验证，聪音的原生语音均为7秒以内的短音频，且无背景伴奏、无混响、无环境杂音，为纯净人声干声，无需额外进行人声分离与音频切片处理；仅需剔除无效音效、过短语气音，最终筛选素材总时长建议3-10分钟，覆盖陈述句、疑问句、感叹句等多种语气，提升模型泛化能力。

### 3. 训练数据集预处理（训练效果核心）
本环节完全对应B站核心训练教程的数据集制作步骤，是决定音色还原度的关键；因解包获取的聪音语音均为7秒以内的纯净人声干声，**直接跳过UVR5人声伴奏分离&去混响去延迟、语音切分工具处理环节**，仅对前置数据集进行语音识别与语音标注操作：
1.  ASR语音识别与文本标注：使用GPT-SoVITS WebUI内置的「ASR自动标注」功能，为筛选后的单条语音文件生成对应文本内容。
2.  文本100%校对：**必须手动逐句核对每一条音频的标注文本**，保证文本内容与音频发音完全一致，避免训练后模型出现吞字、发音不准、语气不符的问题。

### 4. GPT-SoVITS训练配置
1.  打开GPT-SoVITS-v2pro WebUI，进入「训练」标签页，填写模型名称（仅支持英文/数字，禁止中文、空格、特殊符号）。
2.  按照B站核心训练教程指引，选择训练集路径（预处理完成的音频文件夹）、标注文本路径（校对好的.list标注文件）。
3.  语种选择中文，匹配游戏角色语音环境；v2pro版本必须选择`s2v2Pro.json`专属配置文件，其余参数完全对应B站核心训练教程的推荐值，可根据显卡显存调整批次大小，避免爆显存。

### 5. 分阶段模型训练
本环节完全对应B站核心训练教程的分阶段训练逻辑，聪音角色语音克隆全程参考该教程操作：
1.  **SoVITS模型训练（音色克隆核心）**
    - 确认参数无误后，点击「开启SoVITS训练」，训练轮数参考教程推荐值，游戏短语音素材建议8-10轮，不超过15轮，避免过拟合。
    - 训练完成后，模型会自动保存在`SoVITS_weights`文件夹中。
2.  **GPT模型训练（语义语气适配核心）**
    - 参数设置与SoVITS训练轮数保持一致，点击「开启GPT训练」，等待训练完成。
    - 训练完成后，模型会自动保存在`GPT_weights`文件夹中；本环节训练将让模型适配实时对话的语义与语气，实现自由问答场景下的自然语音生成。

### 6. 模型推理测试与效果验证
1.  进入WebUI「推理」标签页，加载训练完成的SoVITS与GPT模型。
2.  选择训练集内3-10秒的参考音频，填写对应参考文本，选择中文语种。
3.  输入游戏实时对话场景的测试文本，点击「合成语音」，对比训练后语音与游戏原生语音的音色还原度、自然度，验证训练效果。

### 7. API对接与游戏Mod落地
#### 7.1 Mod本体下载与安装
Mod官方下载地址：https://github.com/qzrs777/AIChat/tree/main
1.  进入Mod官方仓库，从`Releases`页面下载最新版`AIChatMod.zip`并解压；也可使用GitHub Actions在线构建的最新预览版。
2.  安装BepInEx前置：在Steam右键《Chill With You》-> 管理 -> 浏览本地文件，将压缩包内`BepInEx_*`文件夹下的内容复制到游戏根目录，运行一次游戏生成插件目录结构。
3.  确认游戏目录下已生成`BepInEx/plugins`文件夹，将压缩包内的`AIChat.dll`放入该文件夹，完成Mod安装。

#### 7.2 训练模型与Mod对接配置
1.  按照B站核心训练教程的步骤，启动GPT-SoVITS-v2pro的WebAPI v2服务，默认运行地址为`http://127.0.0.1:9880`。
2.  打开游戏，按F9/F10键调出Mod界面，在TTS配置项中，填写TTS服务URL为上述API地址，替换默认参考音频为你训练使用的角色参考音频，填写对应参考文本与语种。
3.  在LLM配置中填写兼容的API地址、Key与模型名称，保存配置后，即可在游戏内测试对话，验证AI角色使用训练后专属语音完成实时问答的效果，完成全流程闭环。

---

## ASR语音识别标注终端运行说明
点击WebUI内语音识别标注功能后，GPT-SoVITS-v2pro终端将自动执行以下流程，终端运行完整日志与说明如下：
```
[INF0] Added DLL directory: D:\AIgju\GPT-SoVITS-v2pro-20250604\runtime\lib\site-packages\torch\Lib
[INF0] Loaded: cudnn_cnn_infer64_8.dll
[INF0] Loaded: cudnn_cnn_train64_8.dll
Downloading model from ModelScope: XXXXRT/faster-whisper to tools/asr/models
Downloading Model from https://www.modelscope.cn to directory: D:\AIgju\GPT-SoVITS-v2pro-20250604\tools\asr\models
2026-03-01 12:23:58, 249 - modelscope - INFO - Got 5 files, start to download
Downloading [faster-whisper-large-v3-turbo/config.json]: 100%
Downloading [faster-whisper-large-v3-turbo/preprocessor_config.json]: 100%
Downloading [faster-whisper-large-v3-turbo/tokenizer.json]: 100%
Downloading [faster-whisper-large-v3-turbo/vocabulary.json]: 100%
Downloading [faster-whisper-large-v3-turbo/model.bin]: 100%
Processing 5 items: 100%
2026-03-01 12:31:33, 299 - modelscope - INFO - Download model 'XXXXRT/faster-whisper' successfully.
loading faster whisper model: tools/asr/models/faster-whisper-large-v3-turbo
```

### 日志核心说明
1.  **依赖库加载**：程序会自动加载CUDA/cudnn相关的GPU加速依赖库，为语音识别提供硬件加速支持。
2.  **模型自动下载**：首次执行ASR语音标注时，程序会自动从ModelScope平台下载`faster-whisper-large-v3-turbo`语音识别模型，包含配置文件、分词器、词表、1.51G大小的模型主体文件，下载完成后自动保存到`tools/asr/models/`目录。
3.  **模型加载**：下载完成后，程序会自动加载语音识别模型，加载完成后即可开始批量执行音频文件的文本标注工作。

---

## 常见问题与避坑指南
### 解包环节
1.  重构版AssetStudio仅支持标准Unity/UnityCN资源，若出现资源无法解析，可参考工具原作者视频排查是否为魔改加密资源。
2.  提取的游戏资源仅可用于个人本地训练，严禁二次传播、商用，避免侵权风险。

### ASR语音标注环节
1.  首次运行标注功能出现长时间下载进度，为正常现象，需等待faster-whisper模型完整下载完成后才会开始识别，请勿关闭终端。
2.  模型下载速度慢/下载失败：可手动从ModelScope下载`faster-whisper-large-v3-turbo`模型，解压后放入`tools/asr/models/`目录，重启程序即可跳过自动下载步骤。
3.  模型加载失败/识别报错：检查GPU驱动是否正常，CUDA版本是否匹配GPT-SoVITS-v2pro要求，也可将模型`compute_type`参数调整为`float16`或`int8`降低硬件要求。
4.  识别文本准确率低：优先使用large-v3系列模型，同时确保音频为无杂音的纯净人声，识别完成后必须手动校对文本，避免标注错误影响训练效果。

### 训练环节
1.  必须使用v2pro版本配套的预训练模型，不可使用旧版v1的预训练模型，否则会出现训练报错、无法对接Mod的问题。
2.  训练后音色不还原，优先排查数据集：文本标注是否100%准确、素材是否覆盖多种语气、是否剔除了无效的音效/非人声片段。
3.  显存不足时，优先降低音频切片长度与训练批次大小，不要强行调高参数，避免爆显存。
4.  训练轮数不可过高，否则会出现过拟合，导致模型仅能还原固定台词，无法适配自由对话场景。

### 对接与Mod环节
1.  实时对话出现吞字、重复、语气生硬，优先更换更低轮数的模型，或缩短输入文本长度。
2.  对接Mod前需先在WebUI内完成推理测试，确认模型无问题后再开启API接口，避免对接后出现异常。
3.  Mod不生效/找不到plugins文件夹：先运行一次游戏生成完整目录结构，再将`AIChat.dll`放入对应文件夹；Linux用户需在Steam启动项中添加`WINEDLLOVERRIDES="winhttp=n,b" %command%`加载前置。
4.  TTS无声音/报错：先通过浏览器访问API测试链接验证TTS服务是否正常，再检查Mod内TTS服务地址、参考音频路径、语种配置是否正确，详细日志可查看游戏目录下`BepInEx/LogOutput.log`。
5.  AI返回内容格式异常：需使用符合Mod要求的系统提示词，强制AI按`[Emotion] ||| 语音文本 ||| 中文字幕`的格式输出，否则将无法正常调用TTS。

---

## 开源协议
本项目的原创教程内容基于 **MIT协议** 开源，你可以自由使用、修改、分发本教程的原创内容，但必须保留原作者署名与本免责声明。
所有引用的第三方内容、工具、Mod、游戏资源的版权归原作者/原厂商所有，不适用本协议。
