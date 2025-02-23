from collections import defaultdict

def check_subgraphs(data):
    # Extract nodes
    nodes = set(node["node_id"] for node in data["requests"]["nodes"])
    
    # Build adjacency list
    edges = defaultdict(set)
    for predicate in data["requests"]["predicates"]:
        source, target = predicate["source"], predicate["target"]
        edges[source].add(target)
        edges[target].add(source)

    # Function to traverse the graph using DFS
    def dfs(start_node, visited, subgraph):
        stack = [start_node]
        while stack:
            node = stack.pop()
            if node not in visited:
                visited.add(node)
                subgraph.add(node)
                stack.extend(edges[node] - visited)
        return subgraph

    visited = set()
    subgraphs = []

    # Identify distinct subgraphs
    for node in nodes:
        if node not in visited:
            subgraph = set()
            subgraph = dfs(node, visited, subgraph)
            subgraphs.append(subgraph)

    # Debugging: Print detected subgraphs
    print(f"Subgraphs detected: {len(subgraphs)}")
    for i, subgraph in enumerate(subgraphs, 1):
        print(f"Subgraph {i}: {subgraph}")

    # If there's more than one subgraph, raise an error
    if len(subgraphs) > 1:
        raise ValueError(f"Error: More than one subgraph detected ({len(subgraphs)} subgraphs).")

# Example JSON data#
 