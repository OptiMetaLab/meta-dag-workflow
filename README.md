# meta_dag_workflow
We generate fully reproducible synthetic DAG workloads for heterogeneous scene and avatar tasks, where each DAG enforces acyclic connectivity, contains one mandatory scene node, and nodes carry multi-dimensional attributes sampled from predefined ranges, with topology and density controlled via deterministic seeding.

This project provides **a DAG workflow dataset for metaverse/virtual scene tasks** and **a Python DAG parser**.
The dataset can be used for task offloading, scheduling algorithms, and resource optimization research. The parser converts **_.gv_** DAG files into actionable task objects and dependency matrices, facilitating simulation and algorithm development.

# **Dataset Description**
The dataset contains synthetic, fully reproducible DAG workflows covering heterogeneous Scene and Avatar tasks.

(i) DAG attributes:
  Number of nodes: 20 / 40 / 80 (depending on experimental scale)
  Node attributes:
    ·size: processing data size
    ·latency: transmission data size
    ·energy: energy consumption
    ·type: Scene or Avatar
    ·color / shape: visualization attributes
    
  Edge attributes:
    ·size: edge weight (communication data size)
    ·color: distinguishes Scene/Avatar

(ii) Dataset structure:

    meta_node_<num_nodes>/
    offload<num_nodes>_<folder_index>/
        <num_nodes>.<folder_index>.<dag_index>.gv  # DAG Graphviz file
        graph/
            <num_nodes>_<folder_index>_<dag_index>.png  # Visualization
            
A total of 2,500 DAGs are included, all fully reproducible.



# **DAG Parser Description**
The project provides a Python parser **_offloading_parser.py_** to parse _**.gv**_ DAG files into task objects and dependency matrices.

Features
(1) DAG File Parsing
  Input: .gv file
  Output: node list, dependency matrix, and edge set

(2) Node Representation
  OffloadingTask class encapsulates node attributes:
  id_name, processing_data_size, transmission_data_size, node_type, depth, energy, etc.

(3) Dependencies & DAG Features
  Dependency matrix: dependency
  Predecessor/successor sets: pre_task_sets, succ_task_sets
  Edge set: edge_set (including source, target, depth, processing size, edge weight, etc.)

(4) Feature Encoding
  Node encoding: encode_point_sequence()
  Edge encoding: encode_edge_sequence()
  Supports sorted encoding: encode_point_sequence_with_ranking(sorted_task)

(5) HEFT-style Task Prioritization
  prioritize_tasks(resource_cluster) computes task priorities based on resource cluster capabilities
  
(6) Cost Statistics
  return_cost_metric() returns mean and standard deviation of all edges in the DAG



# **Quick Start Guide**
The following example demonstrates parsing a DAG file in two steps and viewing basic information:

% 1. Import the parser
from offloading_parser import OffloadingTaskGraph

% 2. Parse a DAG file
dag_file = "meta_node_20/offload20_1/20.1.0.gv"
dag = OffloadingTaskGraph(dag_file)

% View DAG information
print(f"Number of nodes: {dag.task_number}")
print("Node list:")
for task in dag.task_list[:5]:  # Display first 5 nodes
    print(f"ID: {task.id_name}, Type: {task.node_type}, Processing size: {task.processing_data_size}, Transmission: {task.transmission_data_size}")

print("Dependency matrix (first 5x5):")
print(dag.dependency[:5, :5])

% Node features
node_features = dag.encode_point_sequence()
print("Node feature examples:")
print(node_features[:2])  # First two nodes

 Notes:
  Only the **_.gv_** file path is required to parse the DAG
  You can access node list, dependency matrix, node/edge features
  Directly usable for scheduling algorithms, reinforcement learning models, or resource simulation 

# **Citation**
If you use this dataset or parser in your research or project, please cite the GitHub repository link.
