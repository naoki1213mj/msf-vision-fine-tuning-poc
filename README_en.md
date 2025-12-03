# Azure OpenAI GPT-4.1 Vision Fine-tuning PoC

🇺🇸 English | [🇯🇵 日本語](README.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![Azure OpenAI](https://img.shields.io/badge/Azure-OpenAI-0078D4?logo=microsoft-azure)](https://azure.microsoft.com/products/ai-services/openai-service)

A Proof of Concept (PoC) project that fine-tunes Azure OpenAI's GPT-4.1 Vision model for multi-class image classification of steel surface defects.

## 📊 Results Summary

| Model | Classification Accuracy | Improvement |
|-------|-------------------------|-------------|
| GPT-4.1 Baseline Model | 53.45% | — |
| GPT-4.1 Vision Fine-tuned Model | 96.55% | **+43.10%** |

> 🎉 Vision fine-tuning improved classification accuracy by approximately **43 percentage points**.

## 🎯 Use Case

Automated classification of surface defects on hot-rolled steel strips. The model identifies 6 types of defect classes:

| Defect Class | Description |
|--------------|-------------|
| Crazing (Cr) | Fine crack patterns |
| Inclusion (In) | Foreign material inclusions |
| Patches (Pa) | Irregular surface patches |
| Pitted Surface (PS) | Pitted surface marks |
| Rolled-in Scale (RS) | Scale rolled into surface |
| Scratches (Sc) | Surface scratches |

## 📁 Project Structure

```text
msf-vision-fine-tuning-poc/
├── GPT-4.1 Vision Fine-tuning PoC.ipynb  # Main notebook (GPT-4.1)
├── archive/                               # Old notebooks (.gitignore target)
├── NEU-DET/                               # Dataset (download from Kaggle)
│   ├── train/                             # Training data
│   │   ├── annotations/                   # Annotations (XML)
│   │   └── images/                        # Image files
│   └── validation/                        # Validation data
│       ├── annotations/
│       └── images/
├── steel_surface_defects/                 # Preprocessed data
│   ├── class1/ ~ class6/                  # Images by class
│   └── jsonl/                             # Training JSONL files
├── result/                                # Evaluation results (.gitignore target)
│   ├── confusion_matrix_*.png             # Confusion matrix images
│   ├── evaluation_results_*.csv           # Evaluation results CSV
│   └── evaluation_results_*.xlsx          # Evaluation results Excel
├── pyproject.toml                         # Python project configuration
├── uv.lock                                # uv package lock file
├── .env.example                           # Environment variables template
├── .gitignore                             # Git ignore settings
├── LICENSE                                # MIT License
├── README.md                              # Japanese README
└── README_en.md                           # This file (English README)
```

> **Note**: The following are not tracked due to `.gitignore`:
>
> - `.venv/` - Virtual environment
> - `.env` - Environment variables (credentials)
> - `archive/` - Old notebook files
> - `result/` - Evaluation result files
> - `NEU-DET/`, `steel_surface_defects/` - Dataset (large files)
> - `uv.lock` - Package lock file
> - `*.ipynb_checkpoints/` - Notebook checkpoints

## 🚀 Setup

### Prerequisites

- Python 3.12 or higher
- [uv](https://docs.astral.sh/uv/) package manager
- Azure subscription
- Azure OpenAI resource (Sweden Central or North Central US region)

### 1. Clone the Repository

```bash
git clone https://github.com/naoki1213mj/msf-vision-fine-tuning-poc.git
cd msf-vision-fine-tuning-poc
```

### 2. Install Dependencies

```bash
uv sync --dev
```

### 3. Configure Environment Variables

Copy `.env.example` to `.env` and set your Azure credentials.

```bash
cp .env.example .env
```

Edit the `.env` file:

```env
api_key="your-azure-openai-api-key"
azure_endpoint="https://your-resource.openai.azure.com/"
subscription_id="your-subscription-id"
resource_name="your-openai-resource-name"
rg_name="your-resource-group-name"
```

### 4. Prepare the Dataset

Download the dataset from [NEU Surface Defect Database (Kaggle)](https://www.kaggle.com/datasets/kaustubhdikshit/neu-surface-defect-database) and place it in the `NEU-DET/` folder.

## 📓 Running the Notebook

Open and run `GPT-4.1 Vision Fine-tuning PoC.ipynb` in Jupyter Notebook or VS Code.

### Notebook Contents

1. **Environment Setup**: Package imports and Azure authentication
2. **Data Preparation**: Load NEU-DET dataset and convert to JSONL format
3. **File Upload**: Upload training/validation data to Azure OpenAI
4. **Fine-tuning**: Execute GPT-4.1 Vision model fine-tuning job
5. **Deployment**: Deploy the fine-tuned model
6. **Evaluation**: Compare baseline and fine-tuned models
7. **Conclusion**: Confusion matrix, classification report, misclassification analysis

## 🔧 Tech Stack

| Category | Technology |
|----------|------------|
| Language | Python 3.12+ |
| AI Service | Azure OpenAI (GPT-4.1 Vision) |
| Package Manager | uv |
| Data Processing | pandas, numpy |
| Visualization | matplotlib, plotly |
| ML Evaluation | scikit-learn |
| Azure SDK | azure-identity, azure-mgmt-cognitiveservices |

## 📖 References

- [Azure OpenAI Fine-tuning Documentation](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning)
- [NEU Surface Defect Database](http://faculty.neu.edu.cn/songkechen/zh_CN/zdylm/263270/list/)
- [GPT-4.1 Vision Capabilities](https://learn.microsoft.com/azure/ai-services/openai/concepts/models)
- [Fine-tuning Models - Microsoft Learn](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#fine-tuning-models)

## ⚠️ Important Notes

- **Region Restriction**: GPT-4.1 Vision fine-tuning is only available in Sweden Central or North Central US regions (as of December 2025)
- **Cost**: Fine-tuning and model hosting incur Azure charges
- **Auto-deletion**: Deployments not used for 15 days are automatically deleted

> 💡 **Tip**: Region availability and model specifications are updated regularly. Check the [Azure OpenAI documentation](https://learn.microsoft.com/azure/ai-services/openai/concepts/models) for the latest information.

## 🤝 Contributing

Issues and Pull Requests are welcome. For major changes, please open an issue first to discuss your proposal.

## 📄 License

This project is licensed under the [MIT License](LICENSE).

## 👤 Author

- GitHub: [@naoki1213mj](https://github.com/naoki1213mj)
