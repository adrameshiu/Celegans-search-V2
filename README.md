# Celegans-search
Study the connectome structure in C. Elegans by finding paths between a set of neuron classes present.

## Usage

- to use the default values chosen in the code, just use the following command in the terminal

  `python main.py`

- To specify the input parameters through command line, follow these optional arguments

  - `--f`
    - specifies a list of `FROM NEURON CLASSES` to find path from as source
    - specify the neuron classes one after the other(do not enclose in quotes and do not  use commas)
    - default specified in code taken otherwise
  - `--t`
    - specifies a list of `TO NEURON CLASSES` to find path to as target
    - follow similar guidelines as the --f argument
    - default specified in code taken otherwise
  - `--cgi`
    - specifies the class grouping intensity
    - Options are
      - `1`-> **Strong**
        - *should have all possible combinations from source cells to target cells*
      - `2`-> **Moderate(default)**
        - *All cells from source connect to at least one cell from target class*
      - `3`-> **Lenient**
        - *Any one cell in from class, connect to at least 1 cell from target class*
      - `0`-> **Show all graphs**
  - `--c`
    - specifies the max distance cutoff depth to search till(default- 2)
  - `--h`
    - **to get a view of all optional parameters available**

- Example Usage

  ```powershell
  python main.py --f AWB --t AVA AVB --c 2 --cgi 0
  ```

> Inputs : 
>
> - Excel file containing the adjacency matrices
> - a list of from node classes
> - a list of to node classes
> - maximum depth of search
> - class grouping intensity
>
> Outputs :
>
> - paths between from and to classes under `out_files/paths`
> - number of connections in and out of the interneurons in `out_files/neuron_info`
> - Dot files of the network in `out_files/dot_files`

## Dependencies

> Ensure Graphviz and pygraphviz are installed(might be a little complicated on windows)

- GraphViz -> https://graphviz.org/download/
- PyGraphViz -> https://pygraphviz.github.io/documentation/stable/install.html

## Screenshots

### Architecture

> For more details on what happens in the tool, refer the `docs` folder

![Architecture](C:\Users\adity\OneDrive\Documents\IUB\Research\Celegans-search-v2\Celegans-search-V2\docs\screenshots\architecture.JPG)

### Sample Run 1

![Sample Run 1](C:\Users\adity\OneDrive\Documents\IUB\Research\Celegans-search-v2\Celegans-search-V2\docs\screenshots\sample_run1.JPG)



### Sample Run 2

![](C:\Users\adity\OneDrive\Documents\IUB\Research\Celegans-search-v2\Celegans-search-V2\docs\screenshots\sample_run2.JPG)

## Motivations

While talking of studying connectome maps, we intend to identify the synapses and interneurons between source and target neurons, lesion/kill certain interneurons and study if the resultant network has any impact on function(based on the connections between sensory and motor neurons). We intend to study how important a neuron class is for a particular behavior/ability/function. To do this, we need to consider how strong a neuron is, in terms of the number of neuron synaptic connections at the junction. We need to find, common path between multiple source and target neuron classes which can help us discover the critical synapses that connect multiple related classes or clusters of neurons. 

Since the adjacency matrices and connectome maps are defined `neuron cell` wise, but most insights are derived `neuron class` wise, there are various ways we have to analyze how the cells are grouped to classes. It is very hard to understand the overall nature of the connectome by just directly looking at the neuron cells as there are so many connections and it gets very hard to track. So, the cell graph first needs to be built based on the adjacency matrices, then the cells need to be grouped to classes based on the requirements and then we can analyze the paths. 

## Folder Structure

````
Celegans_search
├── docs
│   ├── class_grouping.md
│   ├── define_subgraph_as_view.md.md
│   ├── set up virtual env
├── out_files
│   └── paths
│   └── dot_files
│   └── neuron_details
├── lib
│   └── pre_processor
│   └── graph
│       └── path_finder
│       └── networkx_utils
│       └── class_def
│       └── graph_builder
│       └── filter_graph
│       └── group_classes
│   └── minimizer
│   └── manipulation
│   └── options
│       └── args_options.py
│       └── user_settings.py
│   └── logger
├── main.py
├── LICENSE.txt
├── README.rst
├── requirements.txt
````

## User Options

- define what sheets to import and the colors of nodes in the file `lib/options/user_settings.py`

## Data Source

All input data for the C elegans adjacency weights were sourced from https://wormwiring.org/