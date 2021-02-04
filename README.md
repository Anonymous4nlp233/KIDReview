# KIDReview

This is the repo for the paper [KID-REVIEW: Knowledge-GuIdeD Scientific Review Generation with Oracle Pre-training]()

## Requirements
Requirements for all the libraries are in the **requirements.txt**, please use the right version for each library in order to reproduce our results.

## Dataset
Run the command below to download our dataset.
```
sh prepare_data.sh
```


## Finetune
To finetune the baseline model using oracle extraction, use the following command. The default save directory is *trained_models*, the default save model name is *bart.pthbest*
```python
python finetune.py --source oracle --gpu 2
```
To finetune the citation graph model, use the following command. The default save directory is *trained_models*, the default save model name is *bart_cite.pthbest* 
```python
python finetune.py --source oracle --gpu 2 --citation_graph --prepend 
```
To finetune the concept graph model, use the following command. The default save directory is *trained_models*, the default save model name is *bart_concept.pthbest*
```python
python finetune.py --source oracle --gpu 2 --concept_graph
```
To finetune the model using both citation graph and concept graph, we first reload the model trained by using pure concept graph, and then finetune. Please use the following command. The default save directory is *trained_models*, the default save model name is *bart_cite_concept.pthbest*
```
python finetune.py --source oracle --citation_graph --prepend --concept_graph --reload_from_saved trained_models/bart_concept.pthbest
```
All arguments are in **args.py** file, please check it for more settings.

## Generate
Using vanilla model to generate text. The default output directory is *output*, the default predictions are in the created *pred.txt*.
```python
python generate.py --source oracle --gpu 1 --model_name bart.pthbest 
```
Using citataion graph to generate text.
```python
python generate.py --prepend --source oracle --gpu 1 --citation_graph --model_name bart_cite.pthbest
```
Using concept graph to generate text.
```python
python generate.py --source oracle --gpu 1 --concept_graph --model_name bart_concept.pthbest
```
Using both concept graph and citation graph to generate text.
```python
python generate.py --prepend --source oracle --gpu 1 --citation_graph --concept_graph --model_name bart_cite_concept.pthbest 
```