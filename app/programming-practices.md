# 🤝 Contribution guide

This is quick guide about our programming practices and some useful resources to introduce yourself to them in case you are not familiarized.

## Branch structure 🌳

The app is developed under the [HDA architecture paradigm](https://htmx.org/essays/hypermedia-driven-applications/) and therefore only one repo hosts both the client and the server code. 

### Main branch

This branch contains the code devployed in production, its a stable branch and contains all the releases.

### Iteration branches

We organize our development work in cycles or iterations, each one has its own branch. The iteration branch is merged to main once we finish all the user-stories/features designed for the iteration.

### Task branches

Each iteration contains multiple tasks: new features, fixes, refactors, chores... each development task has its own branch. Once the task is finished the branch is merged to its iteration branch.

## Contribution workflow 🧩

We use a fork based workflow, each developer has its own fork from which they can create a PR to the upstream iteration branch. The workflow is detailed step by step in this [post about working with forks by  Chase Pettit](https://gist.github.com/Chaser324/ce0505fbed06b947d962).

## Good practices in contributions ✨

On top of the fork based workflow we encourage the use of [Conventional Commits specification](https://www.conventionalcommits.org/es/v1.0.0/#especificaci%c3%b3n). We also use[Semantic Versioning](https://semver.org/lang/es/) for our releases.
   
- [Brief tutorial by Justin Brooks](https://www.youtube.com/watch?v=OJqUWvmf4gg)
- [Small intro to Semantic Versioning by Syntax](https://youtu.be/97i9pOa2EyE)
- [Semantic Versioning real life examples by Julie Ng](https://youtu.be/q3qE2nJRuYM) for our releases.


