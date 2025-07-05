# Plot Generation Instructions

Due to NumPy 2.x compatibility issues with matplotlib, the plotting code has been separated from the data preparation.
The prepared data files in this directory can be used to generate plots using your preferred plotting tool.

## Available Data Files

1. Model-specific CSV files: `{model}_{learning_rate}.csv`
   - Contains all data for a specific model and learning rate scenario.

2. Comparison data:
   - `loss_comparison.csv`: Loss values across all models and learning rates
   - `accuracy_comparison.csv`: Accuracy values across all models and learning rates
   - `{layer}_comparison.csv`: Embedding layer values for each layer across scenarios

## Recommended Plot Types

1. Line plots comparing loss across all models and learning rates
2. Line plots comparing accuracy across all models and learning rates
3. Grid plots of embedding layer values with color differentiation by scenario
4. Bar plots comparing final accuracy by model and learning rate

## Example Plot Code (when matplotlib is working):

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load loss comparison data
loss_data = pd.read_csv('loss_comparison.csv')

# Reshape for plotting
loss_data_long = loss_data.reset_index().melt(id_vars='epoch', var_name='scenario', value_name='loss')

# Plot
plt.figure(figsize=(12, 8))
sns.lineplot(data=loss_data_long, x='epoch', y='loss', hue='scenario', markers=True)
plt.title('Loss Comparison Across Scenarios')
plt.grid(True, alpha=0.3)
plt.savefig('loss_comparison_plot.png', dpi=300)
```
