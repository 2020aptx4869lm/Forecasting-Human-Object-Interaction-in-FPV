### Get Started
- Follow INSTALL.md for all dependencies
- Download the datasets and unpack them (see ./tools/unpack_*.sh)
- Re-code the videos if necessary (e.g., UCF101 & HMDB51) (see ./tools/recode_videos.sh)
- Convert the datasets into our format (see ./tools/convert_dataset.py). You can also grab the json files from this [link](https://uwmadison.box.com/s/6d3eqefz6rqwij85e5eiau36p43r3pr0) (./parsed_dataset_splits)
- Download pre-trained models (see this [link](https://drive.google.com/drive/folders/1CYWAwoOYRrub9HTSrcpxLpi4Hb7l_vRQ?usp=sharing))
- Try to train on HMDB51. You will need to set up the dataset folders and pre-trained model file in the json config
```shell
python ./train_joint.py ./exp_configs/hmdb51/hmdb51_split1_i3d_res50.json --prec_bn
```
- [Optional]: Distributed training on multiple GPUs using synchronized batch norm. You can use the same config file. Learning rate will be automatically re-scaled.
```shell
python -m torch.distributed.launch --nproc_per_node=NUM_GPUS train.py ./exp_configs/hmdb51/hmdb51_split1_i3d_res50.json -p 5 --prec_bn --sync_bn
```
- Evaluate a trained model. Models are saved in ./ckpt/your_exp/. We recommend report results using the last checkpoint.
```shell
python ./eval_joint.py ./exp_configs/hmdb51/hmdb51_split1_i3d_res50.json --resume your_model
```
- Visualize the training (requires tensorboard)
```shell
tensorboard --logdir ./ckpt/your_exp/logs
```

