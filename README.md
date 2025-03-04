# Task Descriptions for Model and Layer Class Enhancements

## Model Enhancements

### Task 1: Add Feature Transformation (Samyak)

The custom feature transformation in this model applies a simple shift to the node features by adding a constant value to each feature. This transformation is designed to modify the raw features before they are passed through the network layers. Although the example uses a basic addition of 1, such transformations can help adjust the feature distribution, which may improve the model's ability to learn meaningful representations. By shifting or scaling the features in a controlled manner, the model can focus on more relevant aspects of the data and potentially enhance convergence during training. This step can also serve as a foundation for more complex feature manipulations, depending on the specific needs of the task.

### Task 2: Implement Custom Aggregation (Allie)

The custom aggregation in this model applies a weighted transformation to the node features before passing them through the layers. In this case, each node's features are scaled by a constant factor, allowing the model to control the influence of each node's features on the learning process. This aggregation helps adjust the contribution of different node types or features, which can be important for optimizing model performance. By modifying the features in a structured way, the model can ensure that more relevant or important features are emphasized, potentially improving the stability and effectiveness of training, especially in cases with heterogeneous graph structures. This step can also be adjusted or extended for more complex aggregation strategies based on the task at hand.

### Task 3: Implement Custom non-linearity before layers (Aaron)

The custom non-linearity applied before passing through the layers introduces an activation function to modify the node features. In this case, the ReLU (Rectified Linear Unit) activation function is applied to each node's features before they enter the network layers. This non-linearity helps the model capture more complex patterns by introducing a thresholding effect, where negative values are set to zero while positive values remain unchanged. By applying this activation early in the forward pass, the model introduces non-linear transformations that can aid in learning more complex relationships within the data, enhancing the overall expressiveness and performance of the graph neural network.

## Layer Class Enhancements

### Task 4: Implement Normalization on Node Features (Nimrah)

This operation normalizes the node features of each node type in the graph before they are passed through the network. For each node type, if the node data contains features stored under the key 'h', the features are normalized using the L2 norm along the specified dimension (dim=1). Normalization helps standardize the magnitude of the feature vectors, ensuring that no single node's features disproportionately influence the learning process due to large or small values. This step can improve the stability and performance of the model, as normalized features often lead to better convergence during training and help the network focus on relative patterns rather than absolute feature values.

### Task 5: Implement Max Pooling (Dhriti)

This operation introduces a custom aggregation method using max pooling as an alternative to the default mean aggregation. For each edge type in the graph, the node features are first copied using a specified feature name ('Wh_%s' % etype), and then the max pooling operation is applied across the neighboring nodes' features. Specifically, instead of averaging the features (as done with the mean aggregation), max pooling selects the maximum value for each feature across neighboring nodes. This approach can help highlight the most prominent feature values in the neighborhood, which may be useful in cases where the most significant or extreme feature values are more informative than the average. By using max pooling, the model can better capture dominant features in the graph, potentially improving its ability to learn from highly variable or sparse data.

### Task 6: Node Scaling Factor (Sachin)

This operation introduces an additional feature scaling method that applies different scaling factors to node features based on the node type. For each node type in the graph, if the node data contains features stored under the key 'h', a scaling factor is applied to the features. The scaling factor is retrieved from the scaling_factors dictionary, where different values are assigned to specific node types (e.g., 1.2 for 'type1' and 0.8 for 'type2'). However, 'type1' and 'type2' can be any node type in the graph, and the scaling factors can be adjusted based on the specific needs of the model or task. If a node type is not listed in the dictionary, a default scaling factor of 1 is applied, meaning no scaling occurs for those node types. This scaling method helps adjust the influence of different node types by amplifying or reducing their feature values, which can be important for optimizing the model's ability to learn meaningful representations and improving overall performance, especially when different node types have inherently different characteristics or importance.

