# sprout-wrap

[![Build Status](https://travis-ci.org/pivotal-sprout/sprout-wrap.png?branch=master)](https://travis-ci.org/pivotal-sprout/sprout-wrap)

This project uses [soloist](https://github.com/mkocher/soloist) and [librarian-chef](https://github.com/applicationsonline/librarian-chef)
to run a subset of the recipes in sprout's [cookbooks]((https://github.com/pivotal-sprout/sprout).

[Fork it](https://github.com/pivotal-sprout/sprout-wrap/fork) to 
customize its [attributes](http://docs.opscode.com/chef_overview_attributes.html) in [soloistrc](/soloistrc) and the list of recipes 
you'd like to use for your team. You may also want to add other cookbooks to its [Cheffile](/Cheffile), perhaps one 
of the many [community cookbooks](http://community.opscode.com/cookbooks). By default it configures an OS X 
Mountain Lion workstation for Ruby development.

Finally, if you've never used Chef before - we highly recommend you buy &amp; watch [this excellent 17 minute screencast](http://railscasts.com/episodes/339-chef-solo-basics) by Ryan Bates. 

## Installation under Mountain Lion (OS X 10.8) and Mavericks (OS X 10.9)

### The Easy Way:

#### 1. Run bootstrap script

Open a terminal and run:

    \curl -Ls http://git.io/kyeeCg | bash


### The Semi-Manual Way:

#### 1. Install XCode

[![Xcode - Apple](http://r.mzstatic.com/images/web/linkmaker/badge_macappstore-lrg.gif)](https://itunes.apple.com/us/app/xcode/id497799835?mt=12&uo=4)

#### 2. Install Command Line Tools
  
  XCode > Preferences > Downloads
  
#### 3. Clone this project
  
    git clone https://github.com/pivotal-sprout/sprout-wrap.git
    cd sprout-wrap
  
#### 4. Install soloist & and other required gems

    sudo gem install bundler
    bundle

#### 5. Run soloist
  
    bundle exec soloist

## Configuration

This project is a fork of [sprout-wrap](https://github.com/pivotal-sprout/sprout).
It uses Chef cookbooks from [Sprout](https://github.com/pivotal-sprout/sprout).  These are installed via librarian-chef.
[soloist](https://github.com/mkocher/soloist) runs [chef-solo](http://docs.opscode.com/chef_solo.html).

Soloist provides an easy way to configure a [run list](http://docs.opscode.com/essentials_node_object_run_lists.html) and [attributes](http://docs.opscode.com/essentials_cookbook_attribute_files.html) for the chef-solo run: `soloistrc`
This is just a simple YAML file that looks like:

    recipes:
      - bash::prompt
    node_attributes:
      bash:
        prompt:
          color: p!nk

Wondering what attributes to use?

Please see the [attributes files](https://github.com/trinitronx/sprout/tree/master/sprout-osx-apps/attributes) in the various cookbooks in [Sprout](https://github.com/trinitronx/sprout)

## Troubleshooting

There is one prerequisite to watch out for if you are using the `pivotal_workstation::git_projects` to auto-checkout our private repos.
You will need to setup an ssh key to use in order for chef-solo to checkout the private repos.
For this reason we have chosen to add this to our default [COE](http://en.wikipedia.org/wiki/Common_Operating_Environment))

#### 1. Setup Github SSH key

Make sure you have a github account and [ssh key set up](https://help.github.com/articles/generating-ssh-keys)

To avoid SSH key passphrase prompts during soloist run, use:

    eval $(ssh-agent -s)
    ssh-add -K

