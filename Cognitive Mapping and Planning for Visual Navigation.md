#  Cognitive Mapping and Planning for Visual Navigation

## Previous Work

- Classic planning algorithms are limited in terms of search abilities, inefficient
- Previous works in DL-based navigation are limited as they map pixels-to-action directly, does not generalize well in new environments

## Idea

- Joint architecture for mapping and planning, therefore able to train at the same time and mapper adapts to the needs of the planner
- Able to plan with partial observations

## Mapper

$f_t = U(W(f_{t-1}, e_t), f_t')$ where $f_t' = \phi(I_t)$

* $f_t$ is free space estimate at timestep $t$
* $I_t$ is image from the camera at timestep $t$
* $\phi$ is convolutional neural network that estimates free space from input image
* $W$ is transform previous timestep $f_{t-1}$
* ​