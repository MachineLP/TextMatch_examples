
TextMatch

TextMatch is a semantic matching model library for QA & text search ...  It's easy to train models and to export representation vectors.


## Models List

|                 Model                  | ...                                                                                                                                                           |
| :------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  Bow  |  |
| TFIDF |  |
| NGRAMTFIDF     |  |
| BERT    |  |
| ALBERT  |  |
| DSSM    |  |


## 
```
cd TextMatch
export PYTHONPATH=${PYTHONPATH}:../TextMatch
```

```python

import sys
from textmatch.models.text_embedding.model_factory_sklearn import ModelFactory



if __name__ == '__main__':
    wordstest_dict = {"0":"我去玉龙雪山并且喜欢玉龙雪山玉龙雪山", "1":"我在玉龙雪山并且喜欢玉龙雪山", "2":"我在九寨沟", "3":"你好"}   #["我去玉龙雪山并且喜欢玉龙雪山玉龙雪山","我在玉龙雪山并且喜欢玉龙雪山","我在九寨沟"]
    testword = "我在九寨沟,很喜欢"
    
    # 基于bow
    mf = ModelFactory( match_models=['bow'] )
    mf.init(words_dict=wordstest_dict)
    bow_pre = mf.predict(testword)
    print ('pre>>>>>', bow_pre) 
    # pre>>>>> {'bow': [('0', 0.2773500981126146), ('1', 0.5303300858899106), ('2', 0.8660254037844388), ('3', 0.0)]}
    
    mf = ModelFactory( match_models=['bow', 'tfidf', 'ngram_tfidf'] )
    mf.init(words_dict=wordstest_dict)
    pre = mf.predict(testword)
    print ('pre>>>>>', pre) 
    # pre>>>>> {'bow': [('0', 0.2773500981126146), ('1', 0.5303300858899106), ('2', 0.8660254037844388), ('3', 0.0)], 'tfidf': [('0', 0.2201159065358879), ('1', 0.46476266418455736), ('2', 0.8749225357988296), ('3', 0.0)], 'ngram_tfidf': [('0', 0.035719486884261346), ('1', 0.09654705406841395), ('2', 0.9561288696241232), ('3', 0.0)]}
    pre_emb = mf.predict_emb(testword)
    print ('pre_emb>>>>>', pre_emb) 
    
    '''
    pre_emb>>>>> {'bow': array([1., 0., 0., 1., 1., 0., 1., 0.]), 'tfidf': array([0.61422608, 0.        , 0.        , 0.4842629 , 0.4842629 ,
       0.        , 0.39205255, 0.        ]), 'ngram_tfidf': array([0.        , 0.        , 0.37156534, 0.37156534, 0.        ,
       0.        , 0.        , 0.29294639, 0.        , 0.37156534,
       0.37156534, 0.        , 0.        , 0.37156534, 0.        ,
       0.        , 0.        , 0.        , 0.        , 0.        ,
       0.        , 0.        , 0.29294639, 0.37156534, 0.        ,
       0.        , 0.        , 0.        , 0.        , 0.        ,
       0.        , 0.        , 0.        , 0.        ])}
    '''
```

