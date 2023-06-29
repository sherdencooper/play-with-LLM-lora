**Multi-GPU Training**

If you are using torch2.0, you can use the following command to run the training script:

```torchrun --nproc_per_node=2 script.py```

Instead, if you are using torch1.13.1, you should use the following command to run the training script:

```python -m torch.distributed.launch --nproc_per_node=2 script.py```

The two commands work in my side. The transformers library still suggest use torch.distributed.launch to run the training script. However, I met the issue 

```ValueError: Some specified arguments are not used by the HfArgumentParser: ['--local-rank=1']```

It is suggested to use torchrun based on [this thread](https://github.com/huggingface/transformers/issues/22171).