# Semantic Search

## The Task
The objective of this assignment is to engineer a novel wikipedia search engine using what you've learned about data collection, infrastructure, and natural language processing.

The task has two **required sections:**
- Data collection
- Search algorithm development

And one **optional section:** 
  - Predictive modeling

![](http://interactive.blockdiag.com/image?compression=deflate&encoding=base64&src=eJxdjrsOwjAMRXe-wlsmRhaQkDoiMSDxBW5slahtHDmGCiH-nfQxtKy-59zruhPfUsAGPjsA56XvMdIRSIbYCZKD_RncENqQuGBQ3S7TidCwxsynjZUZ1T8m4HqvJlXZnhrBJMHBbWlTDHEeSFravYUXQy_E3TKrwbioMKb5z16UmRxfXZurVY_GjegbhqJIjaXm-wNmzE4W)

### Part 1 -- Collection (required)

We want you to query the wikipedia API and **collect all of the articles** under the following wikipedia categories:

* [Machine Learning](https://en.wikipedia.org/wiki/Category:Machine_learning)
* [Business Software](https://en.wikipedia.org/wiki/Category:Business_software)

The raw page text and its category information should be written to a collection on a Mongo server running on a dedicated AWS instance.

We want your code to be modular enough that any valid category from Wikipedia can be queried by your code. You are encouraged to exploit this modularity to pull additional wikipedia categories beyond ML and Business Software. As always, the more data the better. 

**Note:** Both "Machine Learning" and "Business Software" contain a heirarchy of nested sub-categories. Make sure that you pull every single page within each parent category, not just those directly beneath them. Take time to explore wikipedia's organization structure. It is up to you if you want to model this heirarchy anywhere within Mongo, otherwise flatten it by only recording the parent category associated with each page.

**optional**  
Make it so that your code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python download.py #SOME_CATEGORY#
```
This docker command starts a disposable scipy-notebook container for one-time use to run your script, `download.py`. Where `#SOME_CATEGORY#` is the wikipedia category to be downloaded. Read about passing arguments to python scripts here: https://docs.python.org/3/library/sys.html. 

**optional**  
Make it so that your code can query nested sub-categories e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python download.py #SOME_CATEGORY# #NESTING_LEVEL#
```

### Part 2 -- Search (required)

Use Latent Semantic Analysis to search your pages. Given a search query, find the top 5 related articles to the search query. SVD and cosine similarity are a good place to start. 

**optional**  
Make it so that your code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python search.py #SOME_TERM#
```

### Part 3 -- Predictive Model (optional)

In this part, we want you to build a predictive model from the data you've just indexed. Specifically, when a new article from wikipedia comes along, we would like to be able to predict what category the article should fall into. We expect a training script of some sort that is runnable and will estimate a model. 

Make it so that your code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python train.py
```

Finally, you should be able to pass the url of a wikipedia page and it will generate a prediction for the best category for that page, along with a probability of that being the correct category. 

Make it so that your code can be run via a python script e.g.

```bash
$ docker run --rm -v $(pwd):/home/jovyan jupyter/scipy-notebook python predict.py #URL#
```

## Infrastructure

We recommend that you run a MongDB server on a dedicated t2.micro instance. Feel free to run your Jupyter environment either on another instance or locally.


