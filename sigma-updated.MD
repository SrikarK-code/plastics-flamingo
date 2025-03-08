# σ-ProtFlamingo: Enhancing Protein Generation with Order-Independent Autoregression

## Overview

σ-ProtFlamingo extends our ProtFlamingo architecture by integrating concepts from the σ-GPT framework to enable order-independent autoregressive generation. This enhancement allows for more flexible protein sequence generation conditioned on SMILES representations of chemical compounds, with applications in plastic degradation enzyme design.

## Key Enhancements

### Double Positional Encoding
- Separate encodings for input position and output position of each token
- Enables the model to understand both where tokens are and where they should predict next
- Splits the embedding dimension to accommodate both position types

### Order-Based Attention
- Replaces traditional left-to-right causal attention with permutation-based attention
- Tokens can attend to previous tokens in the order sequence, not just in position
- Custom attention masks are created for each sequence based on its generation order

### Curriculum Learning for Order Randomization
- Training begins with a higher proportion of left-to-right sequences
- Gradually increases the proportion of randomly ordered sequences
- Helps the model transition from traditional autoregression to order-independent modeling

### Token-Based Rejection Sampling
- Enables parallel sampling of multiple tokens
- Evaluates candidate tokens under different orders
- Dynamically accepts tokens that fit well with previously generated content
- Reduces generation steps by an order of magnitude compared to standard autoregression

## Advantages Over Standard ProtFlamingo

- **Flexibility**: Generate proteins in any order, not just left-to-right
- **Conditioning**: Support for infilling and arbitrary token conditioning
- **Speed**: Faster generation through token-based rejection sampling
- **Better Modeling**: Improved understanding of the conditional SMILES space through more diverse training approaches

## Applications

This architecture is particularly suited for generating proteins that can degrade specific plastic compounds. By improving both the quality and generation efficiency of candidate proteins, σ-ProtFlamingo accelerates the development of enzymes for environmental remediation.

## Computational Considerations

The enhanced model requires more computational resources during training due to:
- Custom attention mask creation
- Token shuffling and reordering
- More complex positional encoding

However, these costs are offset by the significant reduction in generation steps during inference, making the approach well-suited for production applications where generation speed is critical.
