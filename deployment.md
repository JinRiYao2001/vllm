```bash
vllm serve /home/riyaojin/workspace/ai/llm_models/JinRiYao2001/Huihui-Qwen3-VL-30B-A3B-Instruct-abliterated-AWQ \
  --served-model-name qwen3-vl-30b-awq \
  --dtype bfloat16 \
  --max-model-len 24576 \
  --gpu-memory-utilization 0.92 \
  --cpu-offload-gb 8 \
  --cpu-offload-params experts \
  --enforce-eager \
  --max-num-seqs 1 \
  --limit-mm-per-prompt '{"image": 1, "video": 0}' \
  --host 0.0.0.0 --port 8000
```
当前使用的是uva模式，可以再激进的使用prefetch模型配合gpu graph，可以引入flextensor