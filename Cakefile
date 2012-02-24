path = require "path"
sytemSpawn = require('child_process').spawn

bundles = [
  "https://github.com/msanders/snipmate.vim.git",
  "https://github.com/kchmck/vim-coffee-script.git",
  "https://github.com/digitaltoad/vim-jade",
  "https://github.com/groenewege/vim-less",
  "https://github.com/tpope/vim-markdown.git",
  "https://github.com/Lokaltog/vim-powerline.git",
  "https://github.com/tpope/vim-fugitive.git",
  "https://github.com/scrooloose/nerdtree.git",
  "https://github.com/ervandew/supertab.git"
]

option "-n", "--name [NAME]", "Foldername of the bundle to update"

task 'update', 'Updates vim bundles', (options) ->
  for url in bundles
    name = getFoldername url
    if options.name isnt undefined and options.name isnt name
      console.log "Skipping #{name}"
      continue

    # Wrap in closure
    clone = (name, url) ->
      path.exists name, (exists) ->
        if exists
          spawn 'git', [ 'pull', 'origin', 'master' ], { cwd: name }
        else
          spawn 'git', [ 'clone', url ]
    clone name, url

# Curry the system spawn
spawn = (cmd, args, options) ->
  options = options or {}
  options.customFds = [0,1,2]

  return sytemSpawn cmd, args, options

gitClone = (url) ->
  spawn "git", [ 'clone', url ]

getFoldername = (url) ->
  urlparts = url.split '/'
  last = urlparts[urlparts.length - 1]
  return last.replace /.git$/, ""


