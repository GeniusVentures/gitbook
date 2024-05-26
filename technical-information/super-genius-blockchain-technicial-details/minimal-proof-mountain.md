# Minimal Proof Mountain

Like MMR, the SuperGenius blockchain uses minimal storage and syncing for only the accounts UTXOs. It can be verified from the Genesis Block to the current UTXO(s) for an account.

{% graphviz %}
digraph MMR_IVC {
    node [shape=rectangle, style=filled, color=lightblue];
    
    // Genesis Node
    genesis [label="Genesis Proof"];
    
    // Branch Nodes
    branch1 [label="Branch 1 Proof"];
    branch2 [label="Branch 2 Proof"];
    
    // UTXO Nodes for Branch 1
    utxo1a [label="UTXO 1A"];
    utxo1b [label="UTXO 1B"];
    
    // UTXO Nodes for Branch 2
    utxo2a [label="UTXO 2A"];
    utxo2b [label="UTXO 2B"];
    
    // Edges
    genesis -> branch1;
    genesis -> branch2;
    
    branch1 -> utxo1a;
    branch1 -> utxo1b;
    
    branch2 -> utxo2a;
    branch2 -> utxo2b;
}
{% endgraphviz %}
