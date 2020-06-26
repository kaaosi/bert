# BERT

**\*\*\*\*\* New June 26th, 2020: Training BERT Models \*\*\*\*\***

毕业设计中文文本分类，分为三类，分别为军事、游戏、娱乐，每类下有25000条带标注的新闻标题

数据集来源为今日头条客户端，[项目地址](https://github.com/skdjfla/toutiao-text-classfication-dataset)

[bert源项目](https://github.com/google-research/bert)

[bert中文预训练模型](https://storage.googleapis.com/bert_models/2018_11_03/chinese_L-12_H-768_A-12.zip)

项目训练参考了这个[教程](https://www.jiqizhixin.com/articles/2019-03-13-4)，但是其中又一个很简单但是卡了我很长时间的问题，所以说参考bert源项目的fine tuning更好

bert demo的fine tuning数据集在[这个博客](https://blog.csdn.net/weixin_43948816/article/details/86063235)有百度云链接，因为数据集版权原因，bert源码给的不能直接得到train dev test三个数据集

# 问题记录

问题：参考教程配置之后，最后一步在用shell文件调用run_classifier.py的时候报错
```
bert absl.flags._exceptions.IllegalFlagValueError: flag --data_dir=None: Flag --data_dir must have a value other than None.
./run.sh: line 4: --task_name=mytask: command not found
./run.sh: line 6: --do_train=true: command not found
./run.sh: line 8: --do_eval=true: command not found
./run.sh: line 10: --data_dir=data_dir/: No such file or directory
./run.sh: line 12: --vocab_file=chinese_L-12_H-768_A-12/vocab.txt: No such file or directory
./run.sh: line 14: --bert_config_file=chinese_L-12_H-768_A-12/bert_config.json: No such file or directory
./run.sh: line 16: --init_checkpoint=chinese_L-12_H-768_A-12/bert_model.ckpt: No such file or directory
./run.sh: line 18: --max_seq_length=128: command not found
./run.sh: line 20: --train_batch_size=32: command not found
./run.sh: line 22: --learning_rate=2e-5: command not found
./run.sh: line 24: --num_train_epochs=3.0: command not found
./run.sh: line 25: --output_dir=mytask_output: command not found

```
解决：这个问题卡了很长时间，在网上也搜索了一番，但是没有找到解决方法，之后在[这里](https://blog.csdn.net/selfimpro_001/article/details/102478273)发现了一个一直忽略的点，在教程里面shell脚本每行之间存在空行，而错误也出在了这里，好像shell脚本不能随便加空行和空格。之后，把空行删去就解决了。
