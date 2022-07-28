# Gvim competitive programming C++

Setting for Gvim competitive programming in c++

> **IMPORTANT NOTICE**: this vimrc is for windows only
> I'm currently working on porting it to Unix / MacOS

## Installation

- Install Gvim
- Install Font
- Copy next code in your _vimrc 

```sh
source $VIMRUNTIME/vimrc_example.vim

au GUIEnter * simalt ~x
set hls
set is
set cb=unnamed
set gfn=Fixedsys:h10
set ts=4
set sw=4
set si
cd C:\Users\tmwil\Documents\vimws

inoremap { {}<Left>
inoremap {<CR> {<CR>}<Esc>O
inoremap {{ {
inoremap {} {}

autocmd filetype cpp nnoremap <F9> :w <bar> !g++ -std=c++14 % -o %:r -Wl,--stack,268435456<CR>
autocmd filetype cpp nnoremap <F10> :!%:r<CR>
autocmd filetype cpp nnoremap <C-C> :s/^\(\s*\)/\1\/\/<CR> :s/^\(\s*\)\/\/\/\//\1<CR> $

set nu
augroup numbertoggle
    autocmd!
    autocmd BufEnter,FocusGained,InsertLeave * set rnu
    autocmd BufLeave,FocusLost,InsertEnter * set nornu
augroup END

set diffexpr=MyDiff()
function MyDiff()
  let opt = '-a --binary '
  if &diffopt =~ 'icase' | let opt = opt . '-i ' | endif
  if &diffopt =~ 'iwhite' | let opt = opt . '-b ' | endif
  let arg1 = v:fname_in
  if arg1 =~ ' ' | let arg1 = '"' . arg1 . '"' | endif
  let arg1 = substitute(arg1, '!', '\!', 'g')
  let arg2 = v:fname_new
  if arg2 =~ ' ' | let arg2 = '"' . arg2 . '"' | endif
  let arg2 = substitute(arg2, '!', '\!', 'g')
  let arg3 = v:fname_out
  if arg3 =~ ' ' | let arg3 = '"' . arg3 . '"' | endif
  let arg3 = substitute(arg3, '!', '\!', 'g')
  if $VIMRUNTIME =~ ' '
    if &sh =~ '\<cmd'
      if empty(&shellxquote)
        let l:shxq_sav = ''
        set shellxquote&
      endif
      let cmd = '"' . $VIMRUNTIME . '\diff"'
    else
      let cmd = substitute($VIMRUNTIME, ' ', '" ', '') . '\diff"'
    endif
  else
    let cmd = $VIMRUNTIME . '\diff'
  endif
  let cmd = substitute(cmd, '!', '\!', 'g')
  silent execute '!' . cmd . ' ' . opt . arg1 . ' ' . arg2 . ' > ' . arg3
  if exists('l:shxq_sav')
    let &shellxquote=l:shxq_sav
  endif
endfunction
```

## Development

*Make sure to have [Git](http://git-scm.com/) and
[Node](http://nodejs.org/) installed.*

1. Fork the repo and create a new branch —or just create a new branch if you
    have permissions.

2. Once you have your local copy, install its dependencies:

    ```sh
    $ npm install
    ```

3. Install [Gulp](https://gulpjs.com/):

    ```sh
    $ npm install gulp -g
    ```

4. Install [Browsersync](https://www.browsersync.io/):

    ```sh
    $ npm install browser-sync -g
    ```

5. Run the `dev` task

    ```sh
    $ gulp dev
    ```

    *This will open the "ui" version at
    [http://localhost:3040](http://localhost:3040/) in your default browser.
    The "mobile" version is at
    [http://localhost:3040/mobile](http://localhost:3040/mobile).*

6. Make all necessary changes, and when all is ready, open a PR.

### Code style and formatting

Make sure your code is complying with the following documents:

- [CSS](https://github.com/mercadolibre/css-style-guide)
- [JavaScript](https://github.com/mercadolibre/javascript-style-guide)

## Tests

Run all tests using:

```sh
$ npm test
```

This will run all tests in the terminal using PhantomJS.

Since tests are executed using the Karma test runner, so feel free to run
them in another browser. For example, If you want to use Google Chrome run:

```sh
./node_modules/.bin/karma start --browsers Chrome
```

## Documentation and live demos

For more information, documentation, or to see live demos, check our
[official website](http://chico.mercadolibre.com/).

## Special thanks

- Guille Paz ([@pazguille](https://twitter.com/pazguille)).

## License

© Licensed under the [MIT license](LICENSE.txt).
