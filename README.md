# Learning Semantic Sentence Embeddings using Pair-wise Discriminator

Train a (EDD_LG_Shared) model  for Parapharse Question Generation. 	 For more information, please refer the paper [https://arxiv.org/abs/1806.00807](https://arxiv.org/abs/1806.00807)


### Requirements
This code is written in Lua and requires [Torch](http://torch.ch/). The preprocssinng code is in Python, and you need to install [NLTK](http://www.nltk.org/) if you want to use NLTK to tokenize the question.

- [NLTK] pip install nltk

You also need to install the following package in order to sucessfully run the code.

- [torch-hdf5](https://github.com/deepmind/torch-hdf5)
- [lua-cjson](http://www.kyne.com.au/~mark/software/lua-cjson.php)
- [loadcaffe](https://github.com/szagoruyko/loadcaffe)


### Training

We have prepared everything for you ;)
For **Paraphrase Question Pair**:

##### Download Dataset
We have refered  [HieCoAttenVQA](https://github.com/jiasenlu/HieCoAttenVQA) and []  to prepare our code base.
The first thing you need to do is to download the Quora Question Pairs dataset from the [Quora Question Pair website](https://data.quora.com/First-Quora-Dataset-Release-Question-Pairs) and put the same in the `data` folder. Now we need to do some preprocessing, head over to the `prepro` folder and run
```
$ python quora_prepro.py
```
**Note** The code given above generates json files for 100K question pairs for train, 5k question pairs for validation and 30K question pairs for Test set. 
If you want to change this and instead use only 50K question pairs for training and rest remaining the same, then you need to make some minor changes in the above code. After this step, it will generate the files under the `data` folder. `quora_raw_train.json`, `quora_raw_val.json` and `quora_raw_test.json`

##### Generate Question Features


```
$ python prepro_quora.py --input_train_json ../data/quora_raw_train.json --input_test_json ../data/quora_raw_test.json 
```
to get the question features. This will generate two files in `data/` folder, `quora_data_prepro.h5` and `quora_data_prepro.json`.


##### Train the model

We have everything ready to train the Question paraphrase model. Back to the root directory

```
th train.lua -input_ques_h5 data/quora_data_prepro.h5 -input_json data/quora_data_prepro.json 
```

### Evaluation

```
th eval.lua -input_ques_h5 data/quora_data_prepro.h5 -input_json data/quora_data_prepro.json 
```

##### Evaluate using Pre-trained Model
The pre-trained model can be download [here](https://figshare.com/s/999a13965bbbd1c87cd3)

```
th eval.lua -input_ques_h5 data/quora_data_prepro.h5 -input_json data/quora_data_prepro.json --start_from [model path]
```

##### Metric

To Evaluate Question paraphrase, you need to download the [evaluation tool](https://github.com/tylin/coco-caption). To evaluate Question Pair , you can use script `myeval.py` under `coco-caption/` folder. If you need to evaluate based on BLEU, METEOR, ROUGE and CIDER score . Follow All the instruction from this link [here](https://github.com/tylin/coco-caption) 



[here](https://figshare.com/s/5463afb24cba05629cdf]


### Reference

If you use this code as part of any published research, please acknowledge the following paper

```
@article{patro2018learning,
  title={Learning Semantic Sentence Embeddings using Pair-wise Discriminator},
  author={Patro, Badri N and Kurmi, Vinod K and Kumar, Sandeep and Namboodiri, Vinay P},
  journal={arXiv preprint arXiv:1806.00807},
  year={2018}
}
```

## Contributors

* [Badri N. Patro][1] (badri@iitk.ac.in)
* [Vinod K. Kurmi][2] (vinodkk@iitk.ac.in)
* [Sandeep Kumar][3] (sandepkr@iitk.ac.in)