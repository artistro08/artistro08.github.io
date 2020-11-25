# GitFlow

In order to manage code and prevent as many merge conflicts as possible (trust me they are a pain in the a-- i mean behind) We will use gitflow to manage all code. 

Gitflow uses `feature` branches to manage code based on what you're working on. For example, if you would like to work on a contact page the following feature would be something like `feature/contact-page-updates`. We create these features to mitigate as much confusion as possible. With our stack, these features are paired with Trello Cards, more particularly the name of the card. Each card that we have in Trello should be paired with a feature. There are also other branches like `releases` for master and (or main if you're using GitHub), `hotfix` for simple fixes. Gitflow automatically versions everything out with a 3 decimal layout. (e.g: `1.0.0`)

## Installing Gitflow

There are two ways you can get gitflow. you can install it via command line, or you can use the VS Code extension. 

### Gitflow Via Command Line
To install gitflow:

``` bash
apt install git-flow
```

documentation on how to use it via command line can be found at [:fab fa-github: nive/gitflow](https://github.com/nvie/gitflow/blob/develop/README.mdown)

### Gitflow for VS Code

You can find the following extension with documentation [here](https://marketplace.visualstudio.com/items?itemName=vector-of-bool.gitflow).

## Next Steps
Now that you have gitflow setup, it's time to get into the code structure.

[Code of Conduct :fas fa-arrow-right:](code_of_conduct.md)