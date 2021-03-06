# GitFlow

In order to manage code and prevent as many merge conflicts as possible _(trust me they are a pain in the a-- I mean behind)_, we will use gitflow to manage all code. 

Gitflow uses `feature` branches to manage code based on what you're working on. For example, if you would like to work on a contact page, the following feature would be something like `feature/contact-page-updates`.

?>We create these features to mitigate as much confusion as possible. With our stack, these features are paired with :fab fa-trello:Trello Cards, more particularly the name of the card.<br><br> Each card that we have in :fab fa-trello:Trello should be paired with a feature. There are also other branches like `releases` for master and (or main if you're using GitHub) and `hotfix` for simple fixes. Gitflow automatically versions everything out with a 3 decimal layout if you're using VS Code. (e.g: `1.0.0`)

</br>

## Installing Gitflow

There are many ways you can get gitflow. We will only go over two. You can install it via command line, or you can use the VS Code extension. 

### Gitflow Via Command Line
To install gitflow via command line, run the following command:

``` bash
apt install git-flow
```

?> Documentation on how to use it via command line can be found at [:fab fa-github: nive/gitflow](https://github.com/nvie/gitflow/blob/develop/README.mdown)

### Gitflow for VS Code

You can find the following extension with documentation [here :fas fa-external-link-alt:](https://marketplace.visualstudio.com/items?itemName=vector-of-bool.gitflow).

</br>

## Creating Features

As I said before, features are to be created for every card you're working on in :fab fa-trello:Trello

For example, if you have a card that is titled "Fix Navigation Styling On Mobile", You will need to create a feature called `feature/fix-navigation-styling-on-mobile`. Feature names are to be as close to the counterpart card as possible.

If you're working on a feature that does not have a card, create a clear and concise name for that feature. That way we can reference who did what easily.

?> Features should only be pushed when you are stuck on code and need someone to review it. If this isn't the case, __do not push the feature to the repository__.

</br>

## Next Steps
Now that you have gitflow setup, it's time to get into the Theme Structure.

[Theme Structure :fas fa-arrow-right:](/docs/theme_structure.md)