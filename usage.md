# Preprocess


```

usage: preprocess.py [-h] -train_src TRAIN_SRC -train_tgt TRAIN_TGT -dev_src
                     DEV_SRC -dev_tgt DEV_TGT [-vocab VOCAB]
                     [-src_vocab_size SRC_VOCAB_SIZE]
                     [-tgt_vocab_size TGT_VOCAB_SIZE]
                     [-min_word_count MIN_WORD_COUNT] [-max_len MAX_LEN]
                     [-lower_case] [-share_vocab] -save_data SAVE_DATA

Preprocessing

optional arguments:
  -h, --help            show this help message and exit
  -train_src TRAIN_SRC  Path to training source data
  -train_tgt TRAIN_TGT  Path to training target data
  -dev_src DEV_SRC      Path to devation source data
  -dev_tgt DEV_TGT      Path to devation target data
  -vocab VOCAB          Path to an existing vocabulary file
  -src_vocab_size SRC_VOCAB_SIZE
                        Source vocabulary size
  -tgt_vocab_size TGT_VOCAB_SIZE
                        Target vocabulary size
  -min_word_count MIN_WORD_COUNT
  -max_len MAX_LEN      Maximum sequence length
  -lower_case
  -share_vocab
  -save_data SAVE_DATA  Output file for the prepared data
```



## train

```

usage: train.py [-h] -data_path DATA_PATH [-d_model D_MODEL] [-d_k D_K]
                [-d_v D_V] [-d_ff D_FF] [-n_heads N_HEADS]
                [-n_layers N_LAYERS] [-dropout DROPOUT] [-share_proj_weight]
                [-share_embs_weight] [-weighted_model] [-lr LR]
                [-max_epochs MAX_EPOCHS] [-batch_size BATCH_SIZE]
                [-max_src_seq_len MAX_SRC_SEQ_LEN]
                [-max_tgt_seq_len MAX_TGT_SEQ_LEN]
                [-max_grad_norm MAX_GRAD_NORM]
                [-n_warmup_steps N_WARMUP_STEPS] [-display_freq DISPLAY_FREQ]
                [-log LOG] -model_path MODEL_PATH

Training Hyperparams

optional arguments:
  -h, --help            show this help message and exit
  -data_path DATA_PATH  Path to the preprocessed data
  -d_model D_MODEL
  -d_k D_K
  -d_v D_V
  -d_ff D_FF
  -n_heads N_HEADS
  -n_layers N_LAYERS
  -dropout DROPOUT
  -share_proj_weight
  -share_embs_weight
  -weighted_model
  -lr LR
  -max_epochs MAX_EPOCHS
  -batch_size BATCH_SIZE
  -max_src_seq_len MAX_SRC_SEQ_LEN
  -max_tgt_seq_len MAX_TGT_SEQ_LEN
  -max_grad_norm MAX_GRAD_NORM
  -n_warmup_steps N_WARMUP_STEPS
  -display_freq DISPLAY_FREQ
  -log LOG
  -model_path MODEL_PATH
```

## translate

```
usage: translate.py [-h] -model_path MODEL_PATH -vocab VOCAB -decode_input
                    DECODE_INPUT -decode_output DECODE_OUTPUT
                    [-batch_size BATCH_SIZE] [-beam_size BEAM_SIZE]
                    [-n_best N_BEST] [-max_decode_step MAX_DECODE_STEP]

Translation hyperparams

optional arguments:
  -h, --help            show this help message and exit
  -model_path MODEL_PATH
                        Path to the test data
  -vocab VOCAB          Path to an existing vocabulary file
  -decode_input DECODE_INPUT
                        Path to the source file to translate
  -decode_output DECODE_OUTPUT
                        Path to write translated sequences
  -batch_size BATCH_SIZE
                        Batch size
  -beam_size BEAM_SIZE  Beam width
  -n_best N_BEST        Output the n_best decoded sentence
  -max_decode_step MAX_DECODE_STEP
                        Maximum # of steps for decoding
```


## Example run

python3 preprocess.py -train_src dataset/valid.en -train_tgt dataset/valid.xh -dev_src  dataset/test.tatoeba.en -dev_tgt dataset/test.tatoeba.xh -src_vocab_size 5000 -tgt_vocab_size 5000 -max_len 300 -save_data outdir/processed_new


python3 train.py -data_path outdir/processed_new-train.t7 -model_path outdir/model  -max_epochs 1 -n_warmup_steps 100

python3 translate.py -model_path outdir/model -vocab outdir/processed_new.dict -decode_input dataset/test.wikimedia.copy.en  -decode_output outdir/wikimedia_copy