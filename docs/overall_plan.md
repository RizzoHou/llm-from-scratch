# 整体规划

中文版大纲+中英字幕授课视频↑ 

[第一次课讲义的中文翻译↑](https://blog.csdn.net/Castlehe/article/details/149370666)

[课程主页↑](https://stanford-cs336.github.io/spring2025/)

[课程github组织↑](https://github.com/stanford-cs336)

[官方视频↑](https://www.youtube.com/watch?v=SQ3fZ1sAqXI&list=PLoROMvodv4rOY23Y0BoGoBGgQ1zmU_MT_)

## Schedule

###### Phase 1  CS 336

1\.19 - 3.6 共6周

| 周次 | 时间段 | 课程 | 主题 | 硬件需求 | 使用要求 |
|:---:|----|----|----|----|----|
| Week1 | 1.19-1.26 | Lecture 1-5 | Assignment 1 (basics): Building a Transformer LM | >24 H100 Hours | 非独占 |
| Week2 | 1.27-1.31, 2.9-2.11 | Lecture 6-9 | Assignment 2 (systems): Systems and Parallelism | 单次运行时间短（考虑总时间约10 H100 hrs） | 独占，需要避免DDP干扰，每人单次运行至少需要1node, 2GPUs |
| Week3 | 2.12-2.14 | Lecture 10-11 | Assignment 3 (scaling): Scaling Laws | 无需单独使用GPU | 全局跑一轮所有参数的训练即可，可能需要在H100机器上跑相当一段时间 |
| Week4 | 2.21-2.26 | Lecture 12-16 | Assignment 4 (data): Filtering Language Modeling Data | 单次运行在2 x H100需7h，考虑多次运行可能需要接近40 H100 Hours | 非独占 |
| Week5 | 2.27-3.6 | Lecture 17 | Assignment 5 (alignment): Alignment and Reasoning RL | >64 H100 Hours | 非独占 |

###### Phase 2 2B模型训练 & Bonus实验

时间：开学后3.7 - 3月中旬

清洗数据：洗一洗数据 拿到大一点的数据集 

模型结构：在CS336的模型结构上增大一点 

训练：在5090集群/H100集群上跑几天，不一定跑到收敛 

测试：MMLU、GSM8K等等 

实验：FP4训练

## ~~Budget~~

~~按H100 15r/h，5090 3r/h，运行时长5090为H100两倍计算开销~~

~~粗略按照总计每人140 H100 hrs计算，保守估计按照70h运行+70h开发计算，考虑需要 210 5090 hrs，则单人总价为￥630。如果加上少数对标H100的benchmark（按5h算），则为￥705每人~~

> ~~目前群里42人，总计约￥29610~~

## Evaluation

提交：

* 每个人每个作业开一个Github Repo存代码
* 按照PDF要求提交Code.zip和Writeup.pdf 

测试：

* Auto-Grading
* Writeup部分"Peer-Review" 分组互相看Writeup&提意见找错误
* Leaderbroad，滚榜展示学习进度&完成情况

## Topics

### CS336 Assignment 1 (basics): Building a Transformer LM

##### Lectures

Lecture 1-5 5课时后交作业

##### Assignment

What you will implement


1. Byte-pair encoding (BPE) tokenizer (§2)
2. Transformer language model (LM) (§3)
3. The cross-entropy loss function and the AdamW optimizer (§4)
4. The training loop, with support for serializing and loading model and optimizer state (§5) What you will run
5. Train a BPE tokenizer on the TinyStories dataset.
6. Run your trained tokenizer on the dataset to convert it into a sequence of integer IDs.
7. Train a Transformer LM on the TinyStories dataset.
8. Generate samples and evaluate perplexity using the trained Transformer LM.
9. Train models on OpenWebText and submit your attained perplexities to a leaderboard.

### CS336 Assignment 2 (systems): Systems and Parallelism

##### Lectures

Lecture 6-9 4课时后交作业

##### Assignment

What you will implement.


1. Benchmarking and profiling harness
2. Flash Attention 2 Triton kernel
3. Distributed data parallel training
4. Optimizer state sharding

### CS336 Assignment 3 (scaling): Scaling Laws

##### Lectures

Lecture 10-11 2课时后交作业

##### Assignment

只需要跑一次 用课程仓库提供的模型结构，把下面的参数都跑一遍，然后给一个API返回loss。 • d_model: An integer value between $[64, 1024]$. • num_layers: An integer value between $[2, 24]$. • num_heads: An integer value between $[2, 16]$. • batch_size: An integer value, one of ${128, 256}$. • learning_rate: A float value between $[1e-3, 1e-4]$. • train_flops: An integer value, one of $\{1e13, 3e13, 6e13, 1e14, 3e14, 6e14, 1e15, 3e15, 6e15, 1e16,3e16, 6e16, 1e17, 3e17, 6e17, 1e18\}$.

### CS336 Assignment 4 (data): Filtering Language Modeling Data

##### Lectures

Lecture 12-16 5课时后交作业

##### Assignment

What you will implement.


1. Convert Common Crawl HTML to text.
2. Filter the extracted text with various methods (e.g., harmful content, personal identifiable information, etc.).
3. Deduplicate the training data. What you will run.
4. Train language models on different datasets to better understand the impact of particular processing decisions on performance.

### CS336 Assignment 5 (alignment): Alignment and Reasoning RL

##### Lectures

Lecture 17 4课时后交作业

##### Assignment

###### Part 1 Alignment and Reasoning RL

What you will implement.


1. Zero-shot prompting baseline for the MATH dataset of competition math problems Hendrycks et al.
2. Supervised finetuning, given reasoning traces from a stronger reasoning model (DeepSeek R1, DeepSeekAI et al. 2025).
3. Expert Iteration for improving reasoning performance with verified rewards.
4. Group-Relative Policy Optimization (GRPO) for improving reasoning performance with verified rewards. For those interested, we will have an **entirely optional** part of the assignment on aligning language models to human preferences, which will be released in the next few days.

What you will run


1. Measure Qwen 2.5 Math 1.5B zero-shot prompting performance (our baseline).
2. Run SFT on Qwen 2.5 Math 1.5B with reasoning traces from R1.
3. Run Expert Iteration on Qwen 2.5 Math 1.5B with verified rewards.
4. Run GRPO on Qwen 2.5 Math 1.5B with verified rewards.

###### Part 2 CS336 Assignment 5 Supplement (alignment): Instruction Tuning and RLHF

What you will implement.


1. Zero-shot prompting baselines for a variety of evaluation datasets.
2. Supervised fine-tuning, given demonstration data with instruction-response pairs.
3. Direct preference optimization (DPO) for learning from pairwise preference data. What you will run.
4. Measure Llama 3.1 zero-shot prompting performance (our baseline).
5. Instruction fine-tune Llama 3.1.
6. Fine-tune Llama 3.1 on pairwise preference data.