# play-with-LLM-LoRA
a personal note about using LLM LoRA for finetuning

LoRA finetuning is efficient for large-scale LLM, however, there are many hiccups or bumps in the road when playing with LoRA. Thus, I'd like to share some training scripts/problems I met/solutions here. If you find these notes helpful, plz leave a star!


My running environment: one server with 2 A100 80GB and one server with 3 A40 40GB. However, when playing with QLoRA with A40, loading the 4bit quantized model will cause ```RuntimeError: CUDA error: an illegal memory access was encountered```. I have no idea why this happens. There's an [issue thread](https://github.com/artidoro/qlora/issues/82) discussing this, however, no solution can solve the problem, including downgrading pytorch. I will update this note if I find the reason. Thus, the experiments are running on A100 server.