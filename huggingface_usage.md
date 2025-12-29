# 服务器huggingface 使用

由于数据盘只有 8T，重复下载的大模型会大量占据空间，因此大家将模型保存在共享存储空间：

## 服务器上的预训练大模型统一存到 ``/data/shared/huggingface/models`` 路径下，通过固定路径访问：

```
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "/data/shared/huggingface/models/agentica-org/DeepSWE-Preview-34b"
tokenizer = AutoTokenizer.from_pretrained(model_id)

model = AutoModelForCausalLM.from_pretrained(model_id)
```

### 下载前：查看是否已经有自己需要的模型，可供直接使用

### 下载后：手动将模型权重移动到该路径下
