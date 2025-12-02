# meta_dag_workflow
We generate fully reproducible synthetic DAG workloads for heterogeneous scene and avatar tasks, where each DAG enforces acyclic connectivity, contains one mandatory scene node, and nodes carry multi-dimensional attributes sampled from predefined ranges, with topology and density controlled via deterministic seeding.

· \textbf{Project Overview}

This project provides a DAG workflow dataset for metaverse/virtual scene tasks and a Python DAG parser.
The dataset can be used for task offloading, scheduling algorithms, and resource optimization research. The parser converts .gv DAG files into actionable task objects and dependency matrices, facilitating simulation and algorithm development.
