# vim composer
Manage [composer](https://getcomposer.org) in Vim

```vim
:ComposerRun <args>
```
To run command for example `:ComposerRun validate` run command validate for your json

```vim
:ComposerGet
```
This command exec the installation flow of composer's install. This process require `curl`
Also remeber that it is possibile run this vim command without enter inside the
editor: `$ vim -c 'ComposerGet' -c 'q'`

```vim
:ComposerInstall [--no-dev ..]
```
This command exec `composer install`. Now you can attach after this command a custom callback to exec your personal flow.

```vim
:ComposerInit [--no-dev ..]
```
This command exec `composer init`.

```vim
function! MyCallbackFunction()
    exec ':silent ! ctags -a %'
endfunction
let g:composer_install_callback = "MyCallbackFunction"
```
In this example after every `composer install` I exec a ctags generation

```vim
:ComposerUpdate [--no-dev ..]
```
This command exec `composer update`.

```vim
:ComposerRequireFunc
```
This command exec `composer require <vendor/repository> <version>`.

```vim
:ComposerJSON
```
This command open `composer.json`


```vim
:ComposerKnowWhereCurrentFileIs
```
Instead of use CtrlP directly, this function check if composer's autogenerated files contains exactly one occurrence of curent word. In this case, class file will be opened. CtrlP with current word is called instead. And because is CtrlP wrapper, we suggest to eventually remap the function with <Leader>p

    nnoremap <Leader>p :call g:ComposerKnowWhereCurrentFileIs()<CR>

If zero or more than one occurrences are found, ... a Customizable function will be called. This function is called VimComposerCustomBehavior(). When you press <Leader>p ComposerKnowWhereCurrentFileIs is called. If one file is found it will be opened. If not, this function is called with current word as parameter. If you want, you can call CtrlP. Here an example:

    function! g:VimComposerCustomBehavior(currentWord)
        exec "normal \<c-p>" . a:currentWord
    endfunction


## Install
```vim
Bundle 'vim-php/vim-composer'
```

## Force composer phar
This plugin support an autodetach test to check the correct path of composer.phar
If this check fails you can try to force correct path
```
let g:composer_cmd = "/usr/bin/composer"
```
