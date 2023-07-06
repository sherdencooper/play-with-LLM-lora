Running qlora.py (to update after obtaining the results)

|    Setting   | GPU | BatchSize           | Step | loss | GPU Usage | Time |
|:------------:|:---:|---------------------|------|------|-----------|------|
| QLoRA-PP     | 2   |                     | 1875 |      |           |      |
| QLoRA-DDP    | 2   | device=2 bs=8 gas=1 | 1875 |      | 45GB/45GB | 6.2h |
| QLoRA-DDP-DS | 2   |                     | 1875 |      |           |      |