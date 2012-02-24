### What?
By now, everybody knows they should be using (pathogen)[https://github.com/tpope/vim-pathogen] 
to easily install and update vim extensions. This cakefile makes it easy by simply cloning a list
of repositories, or by pulling in the changes when the repository is already cloned.

### Installation

* Make sure you have (coffee-script)[http://coffeescript.org/] installed and git in your $PATH
* Clone this repository into the pathogen bundle folder
	* ~\vimfiles\bundle on windows
	* ~/.vim/bundle on OS X or Linux
	* `git clone https://github.com/thomasvm/vim-bundle-cake.git bundle`
* Adapt the bundles collection you can find in the Cakefile	by adding or removing
  git repositories from the `bundles` list

### Usage  
* Now you can update by doing

    cake update

* Alternatively you can only update a single plugin by providing its name

    cake -n vim-fugitive update
