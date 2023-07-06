# Multi-GPU-Related Notes

## Multi-GPU Training without Accelerate
If you feel better to manage multi-GPU training by yourself, you can refer to the following notes.

### Single GPU Training
Sometimes you may want to run the training script in a single GPU even if you have multiple GPUs. You could set ```os.environ["CUDA_VISIBLE_DEVICES"] = "0"``` on top of the training script. Remember to set this before importing torch and transformers otherwise it will not work and running the script will still use all the GPUs.

### Multi-GPU DDP
Transformers trainer will automatically use PP and use all the GPUs available so you can just run ```python script.py``` by setting ```device_map = "auto"```. You can use the following methods to run the DDP:

If you are using torch2.0, you can use the following command to run the training script:

```torchrun --nproc_per_node=2 script.py```

Instead, if you are using torch1.13.1, you should use the following command to run the training script:

```python -m torch.distributed.launch --nproc_per_node=2 script.py```

The two commands work in my side. The transformers library still suggest use torch.distributed.launch to run the training script. However, I met the issue 

```ValueError: Some specified arguments are not used by the HfArgumentParser: ['--local-rank=1']```

With torch2.0. It is suggested to use torchrun based on [this thread](https://github.com/huggingface/transformers/issues/22171). Also, it is more recommended to use torch2 since there are tons of new features which can accelerate the training process.


**Multi-GPU Training with Accelerate**

It would be much easier to use accelerate to manage multi-GPU training.

Since DeepSpeed ZeRO 3 does not support 4/8 bit optimization, ZeRO 2 is recommended to use. Also, according to [this repo]{https://github.com/lich99/ChatGLM-finetune-LoRA}, try ZeRO 2 and no offload first, unless you encounter OOM.

```ZeRO 2 (no offload) > ZeRO 2 (offload) > ZeRO 3 (no offload) > ZeRO 3 (offload)```