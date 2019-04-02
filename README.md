## Visual Search Engine with Elasticsearch

---

## **Pre-requisites**

1. Install Elasticsearch (app context http://localhost:9200)

   - Make sure it is running, by using
     - On mac - curl http://localhost:9200
   - Get the information by going to the following URL on your browser
     - GET /\_nodes
     - http://localhost:9200/_nodes
     - GET /\_cat/health/?v
     - GET /\_cat/indices?v

2. Optional things to install

   - JSON Viewer (Chrome plugin)

3. Train the model on Google Colab

---

## Notes on Elasticsearch

- **Index**:
  An index is a collection of documents that have somewhat similar characteristics. For example, you can have an index for customer data, another index for a product catalog, and yet another index for order data.
- **Shard**:
  Elasticsearch provides the ability to subdivide your index into multiple pieces called shards. When you create an index, you can simply define the number of shards that you want. Each shard is in itself a fully-functional and independent "index" that can be hosted on any node in the cluster
- **Creating and Deleting an Index**:
  You can use the following APIs
  - DELETE /twitter to delete an index named twitter
  - PUT /customer to create an index named customer
- **List of Indices**

  - GET /\_cat/indices?v

- **Helpful**

  - delete index: curl -XDELETE 'localhost:9200/index_name'
  - delete all indices: curl -XDELETE 'localhost:9200/\_all'
  - delete document : curl -XDELETE 'localhost:9200/index_name/type_name/document_id'

- **Function Score**

  - https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-function-score-query.html
  - **https://www.elastic.co/blog/found-function-scoring**
  - https://discuss.elastic.co/t/custom-score-for-fuzzy-matching-based-on-levenshtein-distance-score/125544

- **List of HTTP Commands**

  - http get :9200/vs-str-ecn/\_count < vs-must-query.json

  - http get :9200/vs-str-ecn/\_search < vs-must-query.json

---

## Gotchas!

- Error: Permission denied @ dir_s_mkdir - /usr/local/Frameworks

  - Fix - run the following command

  ```
    brew doctor
  ```

- No module named 'elasticsearch'
  - Fix - If "conda install elasticsearch" does not work, then do the following
  ```
    pip install elasticsearch
  ```

---

Markdown reference: https://commonmark.org/help/

---

## Code References (and ideas for implementation)

1. https://qbox.io/blog/computing-distance-from-a-reference-point-with-script-fields-and-the-explain-api
2. https://www.linkedin.com/pulse/hacking-elasticsearch-image-retrieval-ashwin-saval/
3. https://discuss.elastic.co/t/problem-computing-euclidean-distance-using-script-score-query/148823
4. Keras Documentation
5. Tensorflow Documentation
6. Kaggle Discussions
7. https://barnesanalytics.com/reverse-image-lookup-out-of-the-box
8. https://www.codementor.io/jimmfleming/how-i-built-a-reverse-image-search-with-machine-learning-and-tensorflow-part-1-8dje8gjm9
9. https://shuaiw.github.io/2017/10/05/reverse-image-search.html
10. https://github.com/ThomasDelteil/VisualSearch_MXNet
11. https://github.com/ernestorx/es-swapi-test/blob/master/ES%20notebook.ipynb
12. HTTPie Documentation
13. https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-function-score-query.html
14. https://discuss.elastic.co/t/custom-score-for-fuzzy-matching-based-on-levenshtein-distance-score/125544

---

## Flow of the project

1. Train the model using Google Colab (on any dataset of your choice, eg- Fashion MNIST)

2. Connect to the Elasticsearch instance using maybe Jupyter Notebook as it comes equipped with a lot of libraries

3. Extract the image feature vectors from the trained model

4. Index the extracted image feature vectors with Elasticsearch

5. Take a test image and pre-process it with the same pipeline as before

6. Extract the features of test image and query it within Elasticsearch

7. Elasticsearch will do category matching and scoring

8. Take the score and retrieve the images found via index with the help of our script
