# Tilted Empirical Risk Minimization

This repository contains the data, code, and experiments for the manuscript


> [Tilted Empirical Risk Minimization]()
>
> Arxiv 2020



We demonstrate that TERM can be used for a multitude of applications, 
such as enforcing fairness between subgroups, 
mitigating the effect of outliers, and handling class imbalance.
 TERM is not only competitive with existing solutions tailored to these individual problems, 
 but can also enable entirely new applications, such as simultaneously addressing outliers and promoting fairness.

# Get Started

### Dependencies

As we apply TERM to a diverse set of real-world applications, the dependencies for different applications can be different.

* If we mention that the code is based on other public codebases, you will need to follow the same setup of those codebases. 
* Otherwise, need the following dependencies (the latest versions will work):
	* python3
	* sklearn
	* numpy
	* matplolib
	* colorsys
	* seaborn
	* scipy
	* cvxpy

# Properties of TERM


### Motivating examles
![](https://user-images.githubusercontent.com/14993256/84578901-4b1bc700-ad97-11ea-9fd8-1c3894fbc0ed.png)
    
These figures illustrate TERM as a function of t: (a) finding a point estimate from a set of 2D samples, (b) linear regression with outliers,
     and (c) logistic regression with imbalanced classes. While positive values of t magnify outliers, negative values suppress them. 
     Setting t=0 recovers the original ERM objective.
 
*(How to generate these figures:
`
cd term/toy_example &
jupyter notebook
`
, and directly run the three notebooks.)*
    
### A toy problem to visualize the solutions to TERM

<p align="center">
  <img width="400" height="300" src="https://user-images.githubusercontent.com/14993256/86414333-9be55800-bc91-11ea-9eee-9c49c0d9014e.png">
</p>

TERM objectives for a squared loss problem with N=3. 
As t moves from -<img src="https://render.githubusercontent.com/render/math?math=\infty"> to +<img src="https://render.githubusercontent.com/render/math?math=\infty">, t-tilted losses recover min-loss (t-->+<img src="https://render.githubusercontent.com/render/math?math=\infty">), avg-loss (t=0), and max-loss (t-->+<img src="https://render.githubusercontent.com/render/math?math=\infty">), and approximate median-loss (for some t). TERM is smooth for all finite t and convex for positive t.

*(How to generate this figure:
`
cd term/properties &
jupyter notebook
`
, and directly run the notebook.)*


# How to run the code for different applications

**1. Robust regression** 

```
cd term/robust_regression
python regression.py --obj $OBJ --corrupt 1 --noise $NOISE
```
where `$OBJ` is the objective and `$NOISE` is the noise level (see code for options).


    
**2. Robust classification**

```
cd term/robust_classification
```

* built upon the public [mentornet codebase](https://github.com/google/mentornet)
* dependencies: same as the dependencies of the [mentornet codebase](https://github.com/google/mentornet)
* usage: see `README` under `term/robust_classification`
    
    
**3. Mitigating noisy annotators**


```
cd term/noisy_annotator/pytorch_resnet_cifar10
python trainer.py --t -2  # TERM
```

* built upon the public [cifar10/cifar100 in pytorch codebase](https://github.com/akamaster/pytorch_resnet_cifar10)
* dependencies: same as the dependencies specified in the above codebase
   

**4. Fair PCA**

```
cd term/fair_pca
jupyter notebook
```
and directly run the notebook `fair_pca_credit.ipynb`.

* built upon the public [fair pca codebase](https://github.com/uthaipon/multi-criteria-dimensionality-reduction)
* we directly extract the pre-processed Credit data dumped from the original [matlab code](https://github.com/samirasamadi/Fair-PCA/blob/master/creditProcess.m), which are called `data.csv`, `A.csv`, and `B.csv` saved under `term/fair_pca/multi-criteria-dimensionality-reduction-master/data/credit/`.
* dependencies: same as the [fair pca code](https://github.com/uthaipon/multi-criteria-dimensionality-reduction)


**5. Handling class imbalance**

```
cd term/class_imbalance
python3 -m mnist.mnist_train_tilting --exp tilting  # TERM, common class=99.5%
```

* built upon the public [LearnReweight codebase](https://github.com/uber-research/learning-to-reweight-examples)
* dependencies: same as the [LearnReweight code](https://github.com/uber-research/learning-to-reweight-examples)
	
	
**6. Variance reduction for generalization**

```
cd term/DRO
python variance_reduction.py --obj $OBJ $OTHER_PARAS  
```
where `$OBJ` is the objective, and `$OTHER_PARAS$` are the hyperparameters associated with the objective (see code for options). We report how we select the hyperparameters along with all hyperparameter values in Appendix E of the paper. For instance, for TERM with `t=50`, run the following:
	
```
python variance_reduction.py --obj tilting --t 50  
```

* `simple_projections.py` is directly taken from the [RobustRegRisk code](https://github.com/hsnamkoong/robustopt)
	

**7. Hierarchical multi-objective tilting**

```
cd term/hierarchical
python mixed_level1.py --imbalance 1 --corrupt 1 --obj tilting --t_in -2 --t_out 10  # TERM_sc
python mixed_level2.py --imbalance 1 --corrupt 1 --obj tilting --t_in 50 --t_out -2 # TERM_ca
```

* `mixed_level1.py`: TERM_{sc}: (sample level, class level)
* `mixed_level2.py`: TERM_{ca}: (class level, annotator level)

 

**8. Fair federated learning**

```
cd term/fair_flearn
bash run.sh tilting 0 0 term_t0.1_seed0 > term_t0.1_seed0 2>&1 &
```
* built upon the public [q-FFL codebase](https://github.com/litian96/fair_flearn)
* download the vehicle dataset following [the README in the q-FFL code](https://github.com/litian96/fair_flearn/tree/master/data/vehicle)
* dependencies: same as those required by the [q-FFL code](https://github.com/litian96/fair_flearn)
    
    	


# References


Please see the [paper]() for more details of TERM as well as a complete list of related work.
    
    

 
    
    
   