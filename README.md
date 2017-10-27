This repository provides both `kubectx` and `kubens` tools.

** this fork ** is the result of some quick digging of mine into kubectl productivity

I basically got stuck at:
 - https://github.com/solsson/kube-shell-docker
 - https://github.com/kubernetes/kubernetes/issues/29322
 - https://github.com/kubernetes/kubernetes/issues/27308
 - https://unix.stackexchange.com/questions/4219/how-do-i-get-bash-completion-for-command-aliases

I don't spend a lot of time switching between contexts. Happens per workday, basically.
But `kubens` from this repo is interesting. However I switch namespace a lot more often
than I do `cd -` and `git checkout -`.

Effects I seek:
 * Bash completion compatible with per-execution kubectl namespace selection.
 * Display clearly in prompt which context I'm in (aliases in kubectx are great).

**`kubectx`** help you switch between clusters back and forth:
![kubectx demo GIF](img/kubectx-demo.gif)

**`kubens`** help you switch between Kubernetes namespaces smoothly:
![kubens demo GIF](img/kubens-demo.gif)

# kubectx(1)

kubectx is an utility to manage and switch between kubectl(1) contexts.

```
USAGE:
  kubectx                   : list the contexts
  kubectx <NAME>            : switch to context
  kubectx -                 : switch to the previous context
  kubectx <NEW_NAME>=<NAME> : create alias for context
  kubectx -h,--help         : show this message
```

### Usage

```sh
$ kubectx minikube
Switched to context "minikube".

$ kubectx -
Switched to context "oregon".

$ kubectx -
Switched to context "minikube".

$ kubectx dublin=gke_ahmetb_europe-west1-b_dublin
Context "dublin" set.
Aliased "gke_ahmetb_europe-west1-b_dublin" as "dublin".
```

`kubectx` supports <kbd>Tab</kbd> completion on bash/zsh shells to help with 
long context names. You don't have to remember full context names anymore.

-----

# kubens(1)

kubens is an utility to switch between Kubernetes namespaces.

```
USAGE:
  kubens                    : list the namespaces
  kubens <NAME>             : change the active namespace
  kubens -                  : switch to the previous namespace
  kubens -h,--help          : show this message
```


### Usage

```sh
$ kubens kube-system
Context "test" set.
Active namespace is "kube-system".

$ kubens -
Context "test" set.
Active namespace is "default".
```

`kubens` also supports <kbd>Tab</kbd> completion on bash/zsh shells.

-----

## Installation

**For macOS:**

:tada: kubectx is now in Homebrew! :confetti_ball:

> Use the [Homebrew](https://brew.sh/) package manager:
>
>     brew install kubectx
>
> this will also set up bash/zsh completion scripts automatically.

Running `brew install` with `--with-short-names` will install tools with names
`kctx` and `kns` to prevent prefix collision with `kubectl` name.

> Note: If you installed kubectx before it was accepted to Homebrew core
> repository, reinstall with:
> `brew untap ahmetb/kubectx && brew uninstall --force kubectx && brew update && brew install kubectx`

**Other platforms:**

- Download the `kubectx` script
- Add it somewhere in your PATH
- Make it executable (`chmod +x`)
- You can also install bash/zsh [completion scripts](completion/) manually.

-----

Disclaimer: This is not an official Google product.


#### Stargazers over time

[![Stargazers over time](https://starcharts.herokuapp.com/ahmetb/kubectx.svg)](https://starcharts.herokuapp.com/ahmetb/kubectx)

