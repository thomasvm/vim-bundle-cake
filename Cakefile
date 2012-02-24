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
  todo = bundles.concat()

  next = ->
    return unless todo.length

    url = todo.shift()
    name = getFoldername url
    if options.name isnt undefined and options.name isnt name
      console.log "Skipping #{name}"
      return next()

    clone = (name, url) ->
      path.exists name, (exists) ->
        if exists
          git = spawn 'git', [ 'pull', 'origin', 'master' ], { cwd: name }
          git.on 'exit', ->
            next()
        else
          git = pawn 'git', [ 'clone', url ]
          git.on 'exit', ->
            next()
    clone name, url
  next()

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


