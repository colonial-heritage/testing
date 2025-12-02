# Colonial Collections: integration data

Monorepo for managing and storing the data of the integration layer of Colonial Collections.

## Steps for adding a new data provider

1. Update the file `organizations.ttl` in the `data-registry` folder. Add the details of the data provider (e.g. name and address). The details will automatically be added to the [Colonial Collections knowledge graph](https://data.colonialcollections.nl/data-hub/knowledge-graph/table?graph=https%3A%2F%2Fdata.colonialcollections.nl%2Forganizations) if you commit the changes using Git

## Steps for adding a new dataset

1. Update the file `dataset-measurements.ttl` in the `data-registry` folder. Add the measurements for the new dataset. The measurements will automatically be added to the [Colonial Collections knowledge graph](https://data.colonialcollections.nl/data-hub/knowledge-graph/table?graph=https%3A%2F%2Fdata.colonialcollections.nl%2Fdataset-measurements) if you commit the changes using Git

## Steps for adding a new dataset to the search engine

1. Create a folder in the root folder. By convention: a lower case name, consisting of the name of the data provider and the name of the dataset. For example: `wereldmuseum-collection-archives`
1. Inside the folder, create a `queries` folder
1. Create the file `iterate.rq` in the `queries` folder. Put a SPARQL query in this file (e.g. by [copying one from the existing files](./wereldmuseum-collection-archives/queries/iterate.rq)). The query defines how the entities in the dataset can be retrieved from a SPARQL endpoint, e.g. the [Colonial Collections knowledge graph](https://data.colonialcollections.nl/data-hub/knowledge-graph)
1. Create the file `generate.rq` in the `queries` folder. Put a SPARQL query in this file (e.g. by [copying one from the existing files](./wereldmuseum-collection-archives/queries/generate.rq)). The query defines how the entities in the dataset must be transformed, e.g. to the data model of the [Colonial Collections search graph](https://data.colonialcollections.nl/data-hub/search-graph)
1. Optionally, create the file `check.rq` in the `queries` folder. Put a SPARQL query in this file (e.g. by [copying one from the existing files](./wereldmuseum-collection-archives/queries/check.rq)). The query detects if the dataset has been changed in the [Colonial Collections knowledge graph](https://data.colonialcollections.nl/data-hub/knowledge-graph). If that is the case, the `iterate.rq` and `generate.rq` queries will be executed. Be aware: a `check` query only makes sense if the date of last modification of the dataset can be retrieved from a SPARQL endpoint
1. Inside the `.github/workflows` folder, create a YAML file (e.g. by [copying one from the existing files](./.github/workflows/wereldmuseum-collection-archives-create-graph.yaml)). By convention: a lower case name, consisting of the name of the data provider, the name of the dataset and the `create-graph` suffix, e.g. `wereldmuseum-collection-archives-create-graph.yaml`. Put a GitHub Action workflow definition in this file. The definition describes which steps must be taken to execute the `iterate.rq`, `generate.rq` and - optionally - the `check.rq` queries. The results of the queries will automatically be added to the [Colonial Collections search graph](https://data.colonialcollections.nl/data-hub/search-graph)
