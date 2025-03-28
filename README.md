# SuperAdapters

Finetune ALL LLMs with ALL Adapeters on ALL Platforms!

## Support

| Model          | LoRA               | QLoRA                | AdaLoRA              | Prefix Tuning           | P-Tuning                | Prompt Tuning           |
|----------------| ------------------ |----------------------|----------------------|-------------------------|-------------------------|-------------------------|
| Bloom          | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| LLaMA          | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| LLaMA2         | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| LLaMA3/3.1/3.2 | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| ChatGLM        | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :ballot_box_with_check: | :ballot_box_with_check: | :ballot_box_with_check: |
| ChatGLM2       | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :ballot_box_with_check: | :ballot_box_with_check: | :ballot_box_with_check: |
| Qwen           | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| Baichuan       | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| Mixtral        | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| Phi            | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| Phi3           | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |
| Gemma          | :white_check_mark: | :white_check_mark:   | :white_check_mark:   | :white_check_mark:      | :white_check_mark:      | :white_check_mark:      |

**You can Finetune LLM on** 
- Windows
- Linux
- Mac M1/2

**You can Handle train / test Data with**
- Terminal
- File
- DataBase

**You can Do various Task**
- CausalLM (default)
- SequenceClassification

*P.S. Unfortunately, SuperAdapters do not support qlora on Mac, please use lora/adalora instead.*

## Requirement

CentOS:

```bash
yum install -y xz-devel
```

Ubuntu:
```bash
apt-get install -y liblzma-dev
```

MacOS:
```bash
brew install xz
```

*P.S. Maybe you should recompile the python with xz* 

```bash
CPPFLAGS="-I$(brew --prefix xz)/include" pyenv install 3.10.0
```

If you want to use gpu on Mac, Please read [How to use GPU on Mac](./MacGPUEnv.md)

*P.S. Please Make sure your MacOS version > 14.0 !*

```shell
pip uninstall torch torchvision torchaudio
pip install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu
pip install -r requirements.txt
```

## LLMs

| Model    | Download Link |
|----------| ---- |
| Bloom    | [https://huggingface.co/bigscience/bloom-560m](https://huggingface.co/bigscience/bloom-560m) |
| LLaMA    | [https://huggingface.co/openlm-research/open_llama_3b_600bt_preview](https://huggingface.co/openlm-research/open_llama_3b_600bt_preview) |
| LLaMA2   | [https://huggingface.co/meta-llama/Llama-2-13b-hf](https://huggingface.co/meta-llama/Llama-2-13b-hf) |
| LLaMA3   | [https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct](https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct) |
| Vicuna   | [https://huggingface.co/lmsys/vicuna-7b-delta-v1.1](https://huggingface.co/lmsys/vicuna-7b-delta-v1.1) |
| ChatGLM  | [https://huggingface.co/THUDM/chatglm-6b](https://huggingface.co/THUDM/chatglm-6b) |
| ChatGLM2 | [https://huggingface.co/THUDM/chatglm2-6b](https://huggingface.co/THUDM/chatglm2-6b) |
| Qwen     | [https://huggingface.co/Qwen/Qwen-7B-Chat](https://huggingface.co/Qwen/Qwen-7B-Chat) |
| Mixtral  | [https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2) |
| Phi      | [https://huggingface.co/microsoft/phi-2](https://huggingface.co/microsoft/phi-2) |
| Phi3     | [https://huggingface.co/microsoft/Phi-3-mini-4k-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct) |
| Gemma    | [https://huggingface.co/alpindale/gemma-2b-it](https://huggingface.co/alpindale/gemma-2b-it) |

## Finetune Data Format

[Here is an example](data/train/example.json)

## Usage

### ChatGLM with lora

```bash
python finetune.py --model_type chatglm --data "data/train/" --model_path "LLMs/chatglm/chatglm-6b/" --adapter "lora" --output_dir "output/chatglm"
```

```bash
python inference.py --model_type chatglm --instruction "Who are you?" --model_path "LLMs/chatglm/chatglm-6b/" --adapter_weights "output/chatglm" --max_new_tokens 32
```

### LLaMa with lora

```bash
python finetune.py --model_type llama --data "data/train/" --model_path "LLMs/open-llama/open-llama-3b/" --adapter "lora" --output_dir "output/llama"
```

```bash
python inference.py --model_type llama --instruction "Who are you?" --model_path "LLMs/open-llama/open-llama-3b" --adapter_weights "output/llama" --max_new_tokens 32
```

### Qwen with lora

```bash
python finetune.py --model_type qwen --data "data/train/" --model_path "LLMs/Qwen/Qwen-7b-chat" --adapter "lora" --output_dir "output/Qwen"
```

```bash
python inference.py --model_type qwen --instruction "Who are you?" --model_path "LLMs/Qwen/Qwen-7b-chat" --adapter_weights "output/Qwen" --max_new_tokens 32
```

Other LLMs are some usage of the above.

### Use Classify Mode

You need to specify task_type('classify') and labels

```bash
python finetune.py --model_type llama --data "data/train/alpaca_tiny_classify.json" --model_path "LLMs/open-llama/open-llama-3b" --adapter "lora" --output_dir "output/llama" --task_type classify --labels '["0", "1"]' --disable_wandb
```

```bash
python inference.py --model_type llama --data "data/train/alpaca_tiny_classify.json" --model_path "LLMs/open-llama/open-llama-3b" --adapter_weights "output/llama" --task_type classify --labels '["0", "1"]' --disable_wandb
```

### Use DataBase

1. You need to install a MySQL, and put the db config into the system env.

Eg. 

```
export LLM_DB_HOST='127.0.0.1'
export LLM_DB_PORT=3306
export LLM_DB_USERNAME='YOURUSERNAME'
export LLM_DB_PASSWORD='YOURPASSWORD'
export LLM_DB_NAME='YOURDBNAME'
```

2. create the necessary tables

[Here is the sql files](./sql/)

```sql
source xxxx.sql
```

- db_iteration: [train/test] The record's set name.
- db_type: [test] The record is whether "train" or "test".
- db_test_iteration: [test] The record's test set name.

3. finetune (use chatglm for example)

```shell
python finetune.py --model_type chatglm --fromdb --db_iteration xxxxxx --model_path "LLMs/chatglm/chatglm-6b/" --adapter "lora" --output_dir "output/chatglm" --disable_wandb
```

4. eval

```shell
python inference.py --model_type chatglm --fromdb --db_iteration xxxxxx --db_type 'test' --db_test_iteration yyyyyyy --model_path "LLMs/chatglm/chatglm-6b/" --adapter_weights "output/chatglm" --max_new_tokens 6
```


## Params

### Finetune

```shell
usage: finetune.py [-h] [--data DATA] [--model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}] [--task_type {seq2seq,classify}] [--labels LABELS]
                   [--model_path MODEL_PATH] [--output_dir OUTPUT_DIR] [--disable_wandb] [--adapter {lora,qlora,adalora,prompt,p_tuning,prefix}] [--lora_r LORA_R] [--lora_alpha LORA_ALPHA]
                   [--lora_dropout LORA_DROPOUT] [--lora_target_modules LORA_TARGET_MODULES [LORA_TARGET_MODULES ...]] [--adalora_init_r ADALORA_INIT_R] [--adalora_tinit ADALORA_TINIT]
                   [--adalora_tfinal ADALORA_TFINAL] [--adalora_delta_t ADALORA_DELTA_T] [--num_virtual_tokens NUM_VIRTUAL_TOKENS] [--mapping_hidden_dim MAPPING_HIDDEN_DIM] [--epochs EPOCHS]
                   [--learning_rate LEARNING_RATE] [--disable_warm_up] [--cutoff_len CUTOFF_LEN] [--val_set_size VAL_SET_SIZE] [--group_by_length] [--logging_steps LOGGING_STEPS] [--load_8bit]
                   [--add_eos_token] [--resume_from_checkpoint [RESUME_FROM_CHECKPOINT]] [--per_gpu_train_batch_size PER_GPU_TRAIN_BATCH_SIZE] [--gradient_accumulation_steps GRADIENT_ACCUMULATION_STEPS]
                   [--weight_decay WEIGHT_DECAY] [--fromdb] [--db_iteration DB_ITERATION] [--db_item_num DB_ITEM_NUM]

Finetune for all.

optional arguments:
  -h, --help            show this help message and exit
  --data DATA           the data used for instructing tuning
  --model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}
  --task_type {seq2seq,classify}
  --labels LABELS       Labels to classify, only used when task_type is classify
  --model_path MODEL_PATH
  --output_dir OUTPUT_DIR
                        The DIR to save the model
  --disable_wandb       Disable report to wandb
  --adapter {lora,qlora,adalora,prompt,p_tuning,prefix}
  --lora_r LORA_R
  --lora_alpha LORA_ALPHA
  --lora_dropout LORA_DROPOUT
  --lora_target_modules LORA_TARGET_MODULES [LORA_TARGET_MODULES ...]
                        the module to be injected, e.g. q_proj/v_proj/k_proj/o_proj for llama, query_key_value for bloom&GLM
  --adalora_init_r ADALORA_INIT_R
  --adalora_tinit ADALORA_TINIT
                        number of warmup steps for AdaLoRA wherein no pruning is performed
  --adalora_tfinal ADALORA_TFINAL
                        fix the resulting budget distribution and fine-tune the model for tfinal steps when using AdaLoRA
  --adalora_delta_t ADALORA_DELTA_T
                        interval of steps for AdaLoRA to update rank
  --num_virtual_tokens NUM_VIRTUAL_TOKENS
  --mapping_hidden_dim MAPPING_HIDDEN_DIM
  --epochs EPOCHS
  --learning_rate LEARNING_RATE
  --disable_warm_up
  --cutoff_len CUTOFF_LEN
  --val_set_size VAL_SET_SIZE
  --group_by_length
  --logging_steps LOGGING_STEPS
  --load_8bit
  --add_eos_token
  --resume_from_checkpoint [RESUME_FROM_CHECKPOINT]
                        resume from the specified or the latest checkpoint, e.g. `--resume_from_checkpoint [path]` or `--resume_from_checkpoint`
  --per_gpu_train_batch_size PER_GPU_TRAIN_BATCH_SIZE
                        Batch size per GPU/CPU for training.
  --gradient_accumulation_steps GRADIENT_ACCUMULATION_STEPS
  --weight_decay WEIGHT_DECAY
  --fromdb
  --db_iteration DB_ITERATION
                        The record's set name.
  --db_item_num DB_ITEM_NUM
                        The Limit Num of train/test items selected from DB.
```

## Generate

```shell
usage: inference.py [-h] [--debug] [--web] [--api] [--instruction INSTRUCTION] [--input INPUT] [--max_input MAX_INPUT] [--test_data_path TEST_DATA_PATH]
                    [--model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}] [--task_type {seq2seq,classify}] [--labels LABELS] [--model_path MODEL_PATH]
                    [--adapter_weights ADAPTER_WEIGHTS] [--load_8bit] [--temperature TEMPERATURE] [--top_p TOP_P] [--top_k TOP_K] [--max_new_tokens MAX_NEW_TOKENS] [--vllm] [--fromdb] [--db_type DB_TYPE]
                    [--db_iteration DB_ITERATION] [--db_test_iteration DB_TEST_ITERATION] [--db_item_num DB_ITEM_NUM]

Inference for all.

optional arguments:
  -h, --help            show this help message and exit
  --debug               Debug Mode to output detail info
  --web                 Web Demo to try the inference
  --api                 API to try the inference
  --instruction INSTRUCTION
  --input INPUT
  --max_input MAX_INPUT
                        Limit the input length to avoid OOM or other bugs
  --test_data_path TEST_DATA_PATH
                        The DIR of test data
  --model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}
  --task_type {seq2seq,classify}
  --labels LABELS       Labels to classify, only used when task_type is classify
  --model_path MODEL_PATH
  --adapter_weights ADAPTER_WEIGHTS
                        The DIR of adapter weights
  --load_8bit
  --temperature TEMPERATURE
                        temperature higher, LLM is more creative
  --top_p TOP_P
  --top_k TOP_K
  --max_new_tokens MAX_NEW_TOKENS
  --vllm                Use vllm to accelerate inference.
  --fromdb
  --db_type DB_TYPE     The record is whether 'train' or 'test'.
  --db_iteration DB_ITERATION
                        The record's set name.
  --db_test_iteration DB_TEST_ITERATION
                        The record's test set name.
  --db_item_num DB_ITEM_NUM
                        The Limit Num of train/test items selected from DB.
```

**Use vllm:**

1. Combine the Base Model and Adapter weight
```
python tool.py combine --model_type llama3 --model_path "LLMs/llama3.1/" --adapter_weights "output/llama3.1/" --output_dir "output/llama3.1-combined/"
```
2. Install the dependencies and start vllm server, [Help Link](./vLLMEnv.md).
3. use option vllm
```
python inference.py --model_type llama3 --instruction "Who are you?" --model_path "/root/SuperAdapters/output/llama3.1-combined" --vllm --max_new_tokens 32
```

## Tool

### Combine Base Model and Adapter weight

```
usage: tool.py combine [-h] [--model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}] [--model_path MODEL_PATH] [--adapter_weights ADAPTER_WEIGHTS]
                       [--output_dir OUTPUT_DIR] [--max_shard_size MAX_SHARD_SIZE]

optional arguments:
  -h, --help            show this help message and exit
  --model_type {llama,llama2,llama3,chatglm,chatglm2,bloom,qwen,baichuan,mixtral,phi,phi3,gemma}
  --model_path MODEL_PATH
  --adapter_weights ADAPTER_WEIGHTS
                        The DIR of adapter weights
  --output_dir OUTPUT_DIR
                        The DIR to save the model
  --max_shard_size MAX_SHARD_SIZE
                        Max size of each of the combined model weight, like 1GB,5GB,etc.
```

```
python tool.py combine --model_type llama --model_path "LLMs/open-llama/open-llama-3b/" --adapter_weights "output/llama/" --output_dir "output/combine/"
```

## Inference Web

Add the "--web" parameter

```shell
python inference.py --model_type phi --model_path "LLMs/phi/phi-2" --web
```

![](media/inference_web.png)

## Inference API

Add the "--api" parameter

```shell
python inference.py --model_type phi --model_path "LLMs/phi/phi-2" --api
```

## Label Web

### Classify

```shell
python web/label.py
```

![](media/label_web_1.png)

### Chat

```shell
python web/label.py --type chat
```

![](media/label_web_2.png)

## Reference

- https://github.com/AGI-Edgerunners/LLM-Adapters
- https://github.com/PhoebusSi/Alpaca-CoT
- https://transformers.run/
- https://www.mikecaptain.com/2023/01/22/captain-aigc-1-transformer/
