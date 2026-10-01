# 被埋掉的资源：城市生活垃圾资源化的跨国比较

项目以世界银行 What a Waste 3.0 国家数据表及 WDI 指标为基础，估算严格符合数据覆盖要求的国家样本中的可资源化组分、资源化处理与参照组提升空间。需要 Python 3.10+；安装依赖和首次下载数据需要外网访问。从本目录（包含 `pyproject.toml`）运行 `python -m pip install -e .` 安装项目，再运行 `python -m buried_resources.pipeline --root .`，下载官方原表、验证格式、产生研究输出及图表。建议使用虚拟环境，Windows 完整命令见[仓库首页](../README.md)。重复运行会复用本地原始文件并检查格式及内容。

交互式主流程位于本目录的 [main_analysis.ipynb](main_analysis.ipynb)。它包含可独立顺序执行的下载、校验、分析、匹配和敏感性检查代码，已保存各阶段图表和运行输出。在同一 Python 环境中执行 `python -m pip install jupyterlab ipykernel` 后，从本目录运行 `python -m jupyter lab main_analysis.ipynb`，选择相同环境的内核并依次执行所有单元。

数据源：

- What a Waste 3.0 国家表及代码本：<https://datacatalog.worldbank.org/search/dataset/0039597/what-a-waste-global-database>，CC BY 4.0。项目保存的下载记录显示原始 Excel 文件为 7,268,712 字节；程序读取国家数据表、代码本和 ISO3 代码。
- WDI API：<https://api.worldbank.org/v2/country/all/indicator/NY.GDP.PCAP.PP.KD?format=json&per_page=20000&date=2015:2024> 与相同端点的 `SP.URB.TOTL.IN.ZS`；前者为 2021 国际元不变价购买力平价人均 GDP，后者为城市人口比例。程序以 JSON 格式读取这两个指标，下载记录保存在 `outputs/source_audit.json`。

输出写入 `outputs/`：`source_audit.json`、`validation.json`、`sample_flow.csv`、`country_metrics.csv`、`peer_matches.csv`、`scenario.csv`、`summary.json` 及 PNG 图。Notebook 还输出 `notebook_sensitivity.csv` 和 `peer_sensitivity.png`。已保存的研究报告位于上一级目录：[Report_BurriedResources.pdf](../Report_BurriedResources.pdf)。

研究口径：组成项和处理份额来自不同调查年份，不能作为物理闭合的物料流量表。可资源化组分定义为厨余、园林垃圾、纸、塑料、金属和玻璃之和；只有组分总和接近 100% 的国家进入主样本。观测资源化仅计回收、堆肥、厌氧消化，焚烧不计入（不能确认发电及利用）。所有份额均以垃圾产生量为分母。优先使用“未收集的垃圾质量比例”计算收集覆盖率，其次使用“全国垃圾质量收集覆盖率”；人口或户数覆盖率不得代替质量覆盖率。处理构成不闭合或回收量超过理论可收集成分的国家被剔除；缺失处理子类只有在处理总和闭合时才按零处理。匹配结果是描述性情景，不是政策干预的因果效果，也不能直接等同于填埋减量。

数据使用应注明：World Bank Group, *What a Waste 3.0* country dataset (2026), CC BY 4.0；World Bank, World Development Indicators。原始 Excel 不再装入仓库，程序下载并保存下载校验信息。
