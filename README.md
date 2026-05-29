# Knowledge Graph Implementation Guide

## Theoretical Overview
A **Knowledge Graph (KG)** is a structured representation of real-world entities and their interrelations. Mathematically, it is modeled as a **directed labeled graph** $G = (V, E)$, where:
- **$V$ (Vertices/Nodes)** represent entities (e.g., People, Organizations, Concepts). Each node can have attributes like `type` or `label`.
- **$E$ (Edges/Links)** represent directed relationships between nodes. Each edge is labeled with a specific predicate (e.g., `works_at`, `acquired`).

Knowledge graphs excel at modeling highly interconnected data, enabling graph algorithms (like centrality, shortest path, and community detection) and complex graph-based querying.

## Code Architecture (`KGB.py`)
This repository contains `KGB.py`, a robust Python script that demonstrates how to construct, analyze, and visualize a Knowledge Graph using standard data science libraries.

### 1. Data Ingestion & Modeling
- **Library**: `pandas`
- **Implementation**: Entities and relationships are defined as tabular data (DataFrames). This mirrors typical enterprise workflows where graph data is extracted from relational databases or CSV files.

### 2. Graph Construction & Analysis
- **Library**: `networkx`
- **Implementation**: We instantiate a `nx.DiGraph()` (Directed Graph).
  - Nodes are populated with a `type` attribute (Person vs. Company).
  - Edges are populated with a `relationship` attribute.
- **Analysis**: The script computes **Degree Centrality** (`nx.degree_centrality`) to identify the most connected entities in the network.
- **Export**: The graph structure is exported to standard `GraphML` format (`output/graph.graphml`) for interoperability with external tools like Gephi or Neo4j.

### 3. Static Visualization
- **Libraries**: `matplotlib`, `networkx`
- **Implementation**: Uses a spring layout (`nx.spring_layout`) to position nodes dynamically. Nodes are color-coded based on their `type`, and edges are annotated with their relationship labels. The output is saved as a high-resolution PNG (`output/graph_visualization.png`).

### 4. Interactive Visualization
- **Library**: `pyvis`
- **Implementation**: The `networkx` graph is translated into a `pyvis.network.Network` object. This generates a standalone HTML file (`output/interactive_graph.html`) containing a physics-based, interactive canvas where users can drag, zoom, and inspect node/edge properties.

## Getting Started
### Prerequisites
Install the required dependencies:
```bash
pip install networkx pandas matplotlib pyvis
```

### Execution
Run the builder script:
```bash
python KGB.py
```
The generated artifacts (GraphML, PNG, HTML) will be placed in the `output/` directory.
