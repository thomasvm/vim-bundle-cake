fs = require "fs"
sytemSpawn = require('child_process').spawn

bundles = [
  "https://github.com/kchmck/vim-coffee-script.git",
  "https://github.com/tpope/vim-markdown.git",
  "https://github.com/Lokaltog/vim-powerline.git",
  "https://github.com/tpope/vim-fugitive.git",
  "https://github.com/scrooloose/nerdtree.git",
  "https://github.com/ervandew/supertab.git",
  "https://github.com/kien/ctrlp.vim.git",
  "https://github.com/vim-scripts/mediawiki.vim.git",
  "https://github.com/gabemc/powershell-vim.git",
  "https://github.com/tpope/vim-rails.git",
  "https://github.com/skammer/vim-css-color.git",
  # "https://github.com/digitaltoad/vim-jade",
  # "https://github.com/groenewege/vim-less",
  # "https://github.com/walm/jshint.vim",
  # For snipmate
  "https://github.com/garbas/vim-snipmate.git",
  "https://github.com/tomtom/tlib_vim.git",
  "https://github.com/MarcWeber/vim-addon-mw-utils.git",
  # "https://github.com/honza/snipmate-snippets.git",
  # Color schemes
  "https://github.com/vim-scripts/darkspectrum.git",
  "https://github.com/vim-scripts/fnaqevan",
  "https://github.com/nanotech/jellybeans.vim",
  "https://github.com/tomasr/molokai.git",
  "https://github.com/noahfrederick/Hemisu.git",
  "https://github.com/jpo/vim-railscasts-theme.git",
  "https://github.com/sjl/badwolf.git"
]

console.green = (text) ->
  green = `'\033[32m'`
  reset = `'\033[0m'`
  console.log (green + text + reset)

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
      fs.exists name, (exists) ->
        if exists
          git = spawn 'git', [ 'fetch', 'origin' ], { cwd: name }
          git.on 'exit', ->
            git = spawn 'git', [ 'reset', '--hard', 'origin/master' ], { cwd: name }
            git.on 'exit', ->
              next()
        else
          git = spawn 'git', [ 'clone', url ]
          git.on 'exit', ->
            next()
    console.green name
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


