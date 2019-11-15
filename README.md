# An Implementation of Our [ISWC Paper](http://iswc2018.semanticweb.org/sessions/towards-empty-answers-in-sparql-approximating-querying-with-rdf-embedding/) in PyTorch

## Introduction

This implementation includes three training codes:  
- #### `iswc_train_for_translation_maintenance.py`

To learn the embedding representation which is expected to maintain well the translation mechanism of TransE.

- #### `iswc_train_for_context_preservation.py`  

To learn the embedding representation of the train graph which faithfully preserves the context information for downstream tasks.

- #### `iswc_train_for_entity_prediction.py`  

To learn the embedding representation which could be utilized to predict the entity according to the context.

Two methods were implemented to sample entity contexts and negative entities for training:

- #### `context_and_negatives_pre.py` 

An offline sampling method based on python dictionaries. Although I name it by "offline", the method could still be called during online training for re-sampling, which is also how the above three codes were implemented. 

- #### `online_batch_retrieve.py`

An online sampling method based on torch tensor computation. 

Although the offline method is more effective, I still implemented a training code for demonstration, i.e., `iswc_train_with_online_context_and_negatives_generation.py` based on the online method.

## Dataset

The input knowledge graph data, i.e., `train.txt`, `valid.txt`, and `test.txt`, should be organized in N-triple format. For example:

```
<http://rdf.freebase.com/ns/m.01qscs>   /award/award_nominee/award_nominations./award/award_nomination/award    <http://rdf.freebase.com/ns/m.02x8n1n>
<http://rdf.freebase.com/ns/m.040db>    /base/activism/activist/area_of_activism        <http://rdf.freebase.com/ns/m.0148d>
<http://rdf.freebase.com/ns/m.02jx1>    /location/location/contains     <http://rdf.freebase.com/ns/m.013t85>
```

## Notice:

Please firstly run `data_preparation.py` to generate intermediate files for the training.

Taking FB15k as an example, the structure of the dataset should be like:

```
ISWC2018_Pytorch/
    datasets/
        FB15k/
            input/
                train.txt
                valid.txt
                test.txt
            output/
                # intermediate files would be under this directory
            result/
                # training result would be under this directory
```

Please kindly cite our paper if this paper and the implementation are helpful.
```
@inproceedings{DBLP:conf/semweb/WangWLCZQ18,
  author    = {Meng Wang and
               Ruijie Wang and
               Jun Liu and
               Yihe Chen and
               Lei Zhang and
               Guilin Qi},
  title     = {Towards Empty Answers in {SPARQL:} Approximating Querying with {RDF}
               Embedding},
  booktitle = {The Semantic Web - {ISWC} 2018 - 17th International Semantic Web Conference,
               Monterey, CA, USA, October 8-12, 2018, Proceedings, Part {I}},
  pages     = {513--529},
  year      = {2018},
  crossref  = {DBLP:conf/semweb/2018-1},
  url       = {https://doi.org/10.1007/978-3-030-00671-6\_30},
  doi       = {10.1007/978-3-030-00671-6\_30},
  timestamp = {Tue, 05 Nov 2019 08:34:51 +0100},
  biburl    = {https://dblp.org/rec/bib/conf/semweb/WangWLCZQ18},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```