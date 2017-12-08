#  Cognitive Mapping and Planning for Visual Navigation

[arxiv](https://arxiv.org/abs/1702.03920)

## Previous Work

- Classic planning algorithms are limited in terms of search abilities, inefficient
- Previous works in DL-based navigation are limited as they map pixels-to-action directly, does not generalize well in new environments

## Idea

- Joint architecture for mapping and planning, therefore able to train at the same time and mapper adapts to the needs of the planner
- Able to plan with partial observations

## Mapper

### Intuitions

$f_t = U(W(f_{t-1}, e_t), f_t')$ where $f_t' = \phi(I_t)$

* $f_t$ is free space estimate at timestep $t$
* $e_t$ is egomotion  (environmental displacement) from timestep $t-1$ to $t$
* $I_t$ is image from the camera at timestep $t$
* $\phi$ is function that estimates free space from input image
* $W​$ is a function to transform previous timestep $f_{t-1}​$
* $U$ is a function to that accumulates free space prediction from current & previous timesteps

### Implementation

* $W$ is implemented using bilinear sampling (Therefore allows backpropagation)

* $\phi$ is implemented using convolutional neural network, only predict free space in the current coordinate frame, autoencoder with residual connections

* $U$ is implemented as follows

  $$f_t = \frac{f_{t-1}c_{t-1} + f_t' c_t'}{c_{t-1} + c_t'}$$, and $$c_t = c_{t-1} + c_t'$$

  where $c_t$ denotes the confidence in timestep t