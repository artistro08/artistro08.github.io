# Getting Started

This is a guideline for how OctoberCMS should be handled. 



!> Use this documentation as a guide on how code should be managed in OctoberCMS. This documentation is provided to make sure code can be created quickly and efficiently when working with others.

?> This guide assumes that you already have a local or virtual server setup and a basic understanding of git. If you do not, I recommend you get [:fab fa-github:laravel/valet](https://github.com/laravel/valet) setup or [:fab fa-github:cpriego/valet-linux](https://github.com/cpriego/valet-linux) to get a local server started. You'll also need to [install git :fas fa-external-link-alt:](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [read the git documentation :fas fa-external-link-alt:](https://git-scm.com/doc)

?> You will need to setup composer on your machine. Composer requires PHP. There are plenty of guides on how to setup composer and PHP online. [Google :fas fa-external-link-alt:](https://www.google.com/search?q=how+to+setup+php+and+composer) is your friend

</br>

## Setting Up

There are two ways to setup your repository for OctoberCMS. You can start from scratch or you can setup an existing one. 

</br>

### From Scratch

?> To setup a new repository you'll be using [:fab fa-github: offline/oc-bootstrapper](https://github.com/OFFLINE-GmbH/oc-bootstrapper). Install this package via composer globally from the [documentation :fas fa-external-link-alt:](https://github.com/OFFLINE-GmbH/oc-bootstrapper/blob/develop/README.md)

#### Git Setup
To get started, we will start a new git repository by running the following code:

``` bash
touch october.yaml
git init
git add README.md
git commit -m "Initialize repository"
git branch -M main ## if you're using GitHub
git remote add origin https://github.com/username/repository.git 
git push -u origin master ## replace 'master' with 'main' if you're using GitHub
```

The above will create a `october.yaml` file for setup, create a new branch, and push it to your git provider. 

#### OctoberCMS Setup
Once you've setup the repository, you'll need to add settings to configure the `october.yaml` file you created in the first step. Use this as a base. <br/>

``` yaml
app:
    url: http://example.test                        # domain that you will use
    locale: en                                      # locale of the project
    debug: true                                     # Debug. Set to off if you plan to run this in production

cms:
    theme: theme-name                               # No spaces. dashes only
    edgeUpdates: false                              # Specify edge updates. More info Here: https://octobercms.com/docs/setup/configuration#edge-updates
    disableCoreUpdates: false             
    enableSafeMode: false                           # prevents the system from editing the code section of the site for CMS Pages
    project: 1234567890ABCDEFG                      # Project ID. Read More Here: https://octobercms.com/help/site/projects

database:
    connection: mysql
    host: localhost
    port: 3306
    username: root
    password: password
    database: database

git:
    deployment: false
    bareRepo: false                                 # Exclude everything except themes and custom plugins in git
    excludePlugins: false                           # Even exclude plugins from your repo. Private plugins will be
                                                    # checkout out again during each "install" run. Be careful!
                                                    # Manual changes to these plugins will be overwritten.

plugins:                                            #initial list of plugins for a basic stack
 - anandpatel.wysiwygeditors
 - indikator.backend
 - inetis.dump
 - janvince.smallrecords
 - martin.forms
 - offline.responsiveimages
 - october.drivers
 - rainlab.blog
 - rainlab.pages
 - samuell.contenteditor
 - toughdeveloper.imageresizer
 - vdlp.redirect
 - vojtasvoboda.twigextensions
 - offline.speedy

mail:
    host: smtp.mailgun.org
    name: User Name
    address: email@example.com
    driver: log

```
<br>
Once done, in your terminal, run this command in the root of the folder where the `october.yaml` file is to setup OctoberCMS.

``` bash
october install
```
<br>

__Congratulations__! You have a fully setup OctoberCMS repository. __Go build something amazing!__

?> Don't forget to commit your changes with `git add .` & `git commit` 

</br>

### Existing Setup

If you have an existing repository that you are setting up, you'll need to do the following:

#### Clone & Checkout the develop branch
``` bash
git clone git@github.com:username/repository.git
````

if you are using HTTPS:

``` bash
git clone https://github.com/username/repository.git
```

Now we will switch the branch to __develop__.
``` bash
git checkout develop
```

#### Change directories
``` bash
cd name_of_checkout_folder
```

#### Duplicate the `.env.example` file and rename it `.env`
``` bash
cp .env.example .env
```

#### Set the `APP_URL` 
Open the `.env` file you just created with you favorite text editor and find this line.

``` env
<!-- this depends on the repository -->
APP_URL=example.test 
```

Change it to whatever you need it to be.
``` env
APP_URL=devingreen.test 
```

#### Delete the value for `APP_KEY`. 
With the `.env` file still open, find this line.

``` env
APP_KEY=Change me!!!
```

Clear the value for this line. We will generate it later. 

``` env
APP_KEY=
```

#### Import The Database
Using your favorite database management tool, import the database associated with the git project. If you haven't created an empty database yet, do so. 

?>Your database needs to be completely clean to import, so make sure you __drop all tables__ before importing

``` bash
mysql -u root -p database_name < database_dump.sql # replace appropriate values
```

#### Set the values of `DB_*` to the database you imported 
In your `.env` file, find the following lines:

``` env
DB_DATABASE=example_database
DB_USERNAME=root
DB_PASSWORD=
```

Update those lines to the database that you've imported to. 

``` env
DB_DATABASE=devingreen
DB_USERNAME=root
DB_PASSWORD=SpidermanLivesAgain <!-- your root password, or whatever you have setup on your system -->
```

#### Install Composer Packages
Install all required vendor files needed for the OctoberCMS install to run

``` bash
composer install
```


#### Setup Storage Folder 
Extract the `storage.zip` (or `storage.tar.gz`) file associated with the project in the root of the project folder. Do NOT overwrite `.gitignore` files.

``` bash
# For zip files. You will be prompted for overwriting files. Choose 'No'
unzip storage.zip

# For tar files
tar -zxvf --keep-old-files storage.tar.gz
```


#### Generate an `APP_KEY`
We need to generate an `APP_KEY` to insert into the `.env` file. Run the following command in the root folder to do so.

``` bash
php artisan key:generate
```

It should output something like:
```
[base64:aashfjasdfhajshfusail=]
```

Copy everything in the brackets `[...]` and paste it in the `.env` file under the `APP_KEY` value

```
APP_KEY=base64:aashfjasdfhajshfusail=
```

<br>

__Congratulations__! You have successfully setup an existing OctoberCMS project!

</br>

## Next Steps
To make sure we work together well, We will setup gitflow. Let's get started.

[Gitflow :fas fa-arrow-right:](/docs/gitflow)