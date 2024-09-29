---
title: Example Markdown
---

You can then embed interactive widget cell outputs inside .ipynb files under `notebooks` using the following notation:

````
:::{figure} #app:example_widget
:name: fig_example_widget
:placeholder: ./figures/example_widget_placeholder.png
Example widget.
:::
````

:::{figure} #app:example_widget
:name: fig_example_widget
:placeholder: ./figures/example_widget_placeholder.png
Example widget.
:::

:::{math}
:label: equation1
\frac{1}{2}
:::

This is a markdown cell referencing [Eq. 1](#equation1), here's another way of writing this $\frac{1}{2}$.

This work is based on [@bekkevold2024ultra]. 