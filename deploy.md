## 激活环境
```bash
source .venv/bin/activate
```


## 启动vllm
```bash
vllm serve /home/riyaojin/workspace/ai/llm_models/JinRiYao2001/Huihui-Qwen3-VL-30B-A3B-Instruct-abliterated-AWQ \
  --served-model-name qwen3-vl-30b-awq \
  --dtype bfloat16 \
  --max-model-len 24576 \
  --gpu-memory-utilization 0.92 \
  --cpu-offload-gb 8 \
  --cpu-offload-params experts \
  --max-num-seqs 1 \
  --enforce-eager \
  --limit-mm-per-prompt '{"image": 1, "video": 0}' \
  --host 0.0.0.0 --port 8000
```
当前使用的是uva模式，可以再激进的使用prefetch模型配合gpu graph，可以引入flextensor


## 调试
```bash
curl -s http://192.168.8.18:8000/v1/chat/completions   -H 'Content-Type: application/json'   -d '{"model":"qwen3-vl-30b-awq","messages":[{"role":"user","content":"用一句话介绍你自己"}],"max_tokens":64}'
```


## prefetch模型
```bash
vllm serve /home/riyaojin/workspace/ai/llm_models/JinRiYao2001/Huihui-Qwen3-VL-30B-A3B-Instruct-abliterated-AWQ \
  --served-model-name qwen3-vl-30b-awq \
  --dtype bfloat16 \
  --max-model-len 4096 \
  --gpu-memory-utilization 0.92 \
  --offload-backend prefetch \
  --offload-group-size 4 \
  --offload-num-in-group 2 \
  --offload-prefetch-step 2 \
  --offload-params experts \
  --max-num-seqs 1 \
  --enforce-eager \
  --limit-mm-per-prompt '{"image": 1, "video": 0}' \
  --host 0.0.0.0 --port 8000
```
