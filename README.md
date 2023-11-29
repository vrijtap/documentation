# Documentation

This repository contains the documentation for project Vrijtap. The markdown files are compiled to a static site using mkdocs and they are then hosted at: [https://vrijtap.github.io/documentation/](https://vrijtap.github.io/documentation/)

## Writing Documentation

When you want to add documentation, you will need to add it to one of the markdown files and push it to a (new) branch created for the component creating it for. This is all done in the 'docs' folder. It is first split into products using sub-folders in which the files represent seperate parts of the product, which describe how to use it.

## Use Policy

When you create a new file in this repository, be sure to also add it into the nav list within 'mkdocs.yml'. Otherwise it would not show up on the generated pages and this would require another compilation. Compiling the pages is done using a Github runner and the project can use the runner for a limited amount of time.

As such, it is also expected that all of the written documentation is merged to the main at once and checked for any incosistencies before accepting the merge. It is not allowed to pass small changes to the main, as this would require the re-compilation of the entire documentation folder, which uses valueable runner time.
