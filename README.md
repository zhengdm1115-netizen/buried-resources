# 被埋掉的资源：城市生活垃圾资源化的跨国比较

基于世界银行 What a Waste 3.0 国家数据与 World Development Indicators（WDI），比较符合数据覆盖要求的国家样本中的可资源化组分、观测资源化水平，以及相似国家参照情景下的提升空间。

## 查看项目

- [研究报告（PDF）](Report_BurriedResources.pdf)：阅读研究方法、图表与结论。
- [分析 Notebook](buried_resources-project/main_analysis.ipynb)：查看分步骤代码、已保存的输出与图表。
- [分析结果](buried_resources-project/outputs/)：查看国家指标、样本筛选、参照组匹配、情景结果及图表。
- [代码与方法说明](buried_resources-project/README.md)：了解数据来源、研究口径和运行方式。

当前保存的 `summary.json` 记录：原始数据包含 217 个国家和经济体，主分析保留 84 个样本，垃圾产生量的参考年份为 2012—2023 年。上述数字来自随项目保存的结果文件。

## 文件结构

```text
.
├── Report_BurriedResources.pdf
└── buried_resources-project/
    ├── README.md
    ├── pyproject.toml
    ├── main_analysis.ipynb
    ├── src/buried_resources/pipeline.py
    ├── data/raw/.gitkeep
    └── outputs/
```

原始下载数据由子项目的 `.gitignore` 排除；程序会在需要时从官方来源下载并保存至 `data/raw/`。仓库保留已有结果，阅读报告和结果无需运行代码。

## 重新运行

需要 Python 3.10 或更新版本。首次运行需要联网下载依赖及原始数据。

在 Windows PowerShell 中，从本仓库根目录运行：

```powershell
cd buried_resources-project
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -e .
.\.venv\Scripts\python.exe -m buried_resources.pipeline --root .
```

在 macOS 或 Linux 中，创建虚拟环境后使用 `.venv/bin/python` 替换上述 Windows Python 路径。

如需交互式运行 Notebook，在 `buried_resources-project` 目录中执行：

```powershell
.\.venv\Scripts\python.exe -m pip install jupyterlab ipykernel
.\.venv\Scripts\python.exe -m jupyter lab main_analysis.ipynb
```

命令行流程会重新生成主要表格与图表；Notebook 另含参照组数量的敏感性检查。重新运行会更新 `outputs/` 下的相应文件。

## 数据与解释边界

数据来源及署名方式见[子项目说明](buried_resources-project/README.md)。研究使用国家层面的混合年份观测，匹配结果是描述性情景；结果不能解释为政策干预的因果效果，也不能直接等同于填埋减量。
