# Poradnik

To jest moja zalecana droga nauki Haseklla.

*Uwaga : Ten poradnik jest przetłumaczony na język Polski, jednak wszystkie pozostałe załączniki są w języku Angielskim*

#### Pamiętaj, nie musisz wszystkego od razu zrozumieć, ważne jest abyś kontynuował swoją naukę, zawsze możesz wrócić do niezrozumiałej części.

##Społeczność

Nasz kanał IRC nazywa się `#haskell-beginners`, znajduje się na serwerze Freenode.

Klient webowy [IRC](http://webchat.freenode.net/).

Nasza [lista dyskusyjna](https://wiki.haskell.org/Mailing_lists).

## Netykieta

Bądź miły i uprzejmy. Będąc złosliwym lub niegrzecznym tylko odstraszysz ludzi, i mogą przez to zrezygnować z dalszej nauki.

Nie opisuj czegoś że jest "łatwe" albo "trywialne". Przez to ludze mogą się poczuć się urażeni. Często ludzie którzy uczą się wolniej są bardziej dokładni (?), jest się z czego cieszyć!

Nie bądź zdziwony jak ktoś czegoś nie potrafi lub nie rozumie. Ludzie mogą poczuć się urażeni a ty tylko podbudujesz swoje ego.

Nie bądź człowiekiem 

Żadnych zachowań kończończych się na -sizm i tym podobnych. Rasizm, Seksizm, Homofobia oraz inne zachowania nie będą tolerowane!

---

Guidelines by [the Hacker School manual](https://www.hackerschool.com/manual). Thanks for releasing it Hacker School.

# Co to Haskell, GHC oraz Cabal ?

Haskell jest to język programowania, standard języka został opisany w tym [raporcie](http://www.haskell.org/onlinereport/haskell2010/). Najbardziej aktualny jest z 2010 roku.

## GHC

[GHC](http://www.haskell.org/ghc/) jest to najpopularniesza metoda pracy z Haskellem. GHC zawiera kompilator, REPL oraz menadżer bibliotek.

## Cabal

[Cabal](https://www.haskell.org/cabal/download.html) zajmuje się zarządaniem projektem oraz zarządza zależnościami. Dzięki temu programowi mozesz instalować projekty, zazwyczaj w trybie "piaskownicy"

Cabal jest odpowiednikiem Ruby Bundlera, Python pip node.js npm, maven itd. GHC zarząda pakietami samoistnie. Cabal tylko wybiera wersje ktora ma zostać zainstalowana.

# Instalacja

## Ubuntu

[This PPA](http://launchpad.net/~hvr/+archive/ghc) is excellent and is what I
use on all my Linux dev and build machines.

Specifically:

```bash
$ sudo apt-get update
$ sudo apt-get install python-software-properties # v12.04 and below
$ sudo apt-get install software-properties-common # v12.10 and above
$ sudo add-apt-repository -y ppa:hvr/ghc
$ sudo apt-get update
$ sudo apt-get install cabal-install-1.20 ghc-7.8.4 happy-1.19.4 alex-3.1.3
```

Nastepnie do zmiennej systemowej `$PATH` dodaj nastepujące scieżki (bash\_profile, zshrc, bashrc, etc):

```
~/.cabal/bin:/opt/cabal/1.20/bin:/opt/ghc/7.8.4/bin:/opt/happy/1.19.4/bin:/opt/alex/3.1.3/bin
```

*Opcjonalnie* Dodatkowo możesz takze dodać `.cabal-sandbox/bin` do twojej scieżki. Kod który akurat piszesz bedzie dostepny z poziomu okna poleceń. Zadziała Ci to jedynie jeśli aktualnie pracujesz w folderze który jest podpięty jako cabal sandbox. 

## Debian

### Using Ubuntu PPA

Aby skonfigurować sobie środowisko możesz użyć tych samych kroków co w przypadku Ubuntu. Jednak będziesz musiał/a wywołać kilka dodatkowych komend. Zaraz po `sudo add-apt-repository -y ppa:hvr/ghc` uruchom :

```bash
$ sudo sed -i s/jessie/trusty/g /etc/apt/sources.list.d/hvr-ghc-jessie.list
```

Dla innych wersji Debiana, po prostu zamień wszystkie `jessie` z twoją wersją 

### Manualna kompilacja

Możesz użyć tego [poradnika](http://www.davesquared.net/2014/05/platformless-haskell.html) został on napisany dla systemu Mac OS X:

Uwagi:

- Ustaw swój prefix zgodnie z konfiguracją ghc.
- Zamiast `cabal-install` pliku binarnego, weź źródła a następnie uruchom skrypt `bootstrap.sh`

## Fedora 21

Aby zainstalować Haskell 7.8.4, musisz pobrać repozytorium z nieoficjalnego źródła (Fedobra 22+ już posiada haskell na oficjalnym repozytorium).

```bash
$ sudo yum-config-manager --add-repo \
> https://copr.fedoraproject.org/coprs/petersen/ghc-7.8.4/repo/fedora-21/petersen-ghc-7.8.4-fedora-21.repo  
$ sudo yum install ghc cabal-install
```
Trzeba zaznaczyć że [petersen/ghc-7.8.4 copr page](https://copr.fedoraproject.org/coprs/petersen/ghc-7.8.4/) ten kompilator (ghc) nie może być zainstalowany wraz z Fedora/EPEL ghc

## Arch Linux

Aby zainstalować Haskell z oficjalnego repozytorium, uruchom 

```bash
$ sudo pacman -S cabal-install ghc happy alex haddock
```

## Gentoo
W przypatku Gentoo, możesz zainstalować indywidualny komponent Haskell Platform poprzez Portage. Jeśli użyjesz `ACCEPT_KEYWORDS=arch` (jako przeciwstawieństwo do `ACCEPT_KEYWORDS=~arch`). Porgate zainstaluje ci jakieś stare wersje różnych rzeczy do Haskella. Mając to na uwadze, przy okazji używania `ACCEPT_KEYWORDS=arch`, dodaj następujące wyrażenie do `/etc/portage/package.keywords`.
    
    dev-haskell/cabal-install
    dev-lang/ghc

jak już wszystko zrobisz możesz przejść do następnego kroku,

```bash
$ emerge -jav dev-lang/ghc dev-haskell/cabal-install
```

Gentoo trzyma "stabilne" (stare) wersje `cabal-install` w drzewnie Portage, będziesz musiał użyć `cabal-install` aby zainstalować ostatnie wersje cabala. Miej na uwadze ze w następującym przykładzie backslashes są umyślnie wprowadzone.

```bash
$ \cabal update                # The backslashes
$ \cabal install cabal-install # are intentional
```

Masz już zainstalowanego cabala z partage, oraz lokalnie na twoim domowym folderze (?). Następnie musisz upewnić się że jak uruchomisz `cabal` w terminalu, to twoja powłoka uruchomi najświeższą wersje. Zapewnie bęziesz musiał uruchomić jeszcze jedną komendę aby skonfigurować sobie powłoke:

```bash
PATH=$PATH:$HOME/.cabal/bin
alias cabal="$HOME/.cabal/bin/cabal"
```

Jeśli nie wiesz jaką powłoke posiadasz, prawdopodnie jest to Bash. Jeśli używasz Basha, plik który musisz edytować znajduje się `~/.bashrc`. Jeśli używasz Z-shell, wtedy twój plik konfiguracyjny znajduje się `~/.zshrc`. Możesz uruchomić następującą komende aby dowiedzieć się jaką masz powłoke

```bash
echo $SHELL | xargs basename
```

Ja używam zsh, więc ta komenda wyświetla mi `zsh` kiedy ją uruchomie.

Jak już ukończysz te wszystkie kroki, musisz zainstalowaćdodatkowe narzędzia `alex` oraz `happy`.

```bash
$ cabal install alex happy
```

Gratulacje! Masz w pełni działające środowisko które umożliwi Ci pracowanie z Haskellem

## Mac OS X

### 10.9

Zainstaluj [Kompilator GHC dla Mac OS X](http://ghcformacosx.github.io/), zawiera ona GHC oraz Cabal. Dodatkowo zawiera to instrukcje jak dodac GHC i Cabal do scieżki, zaraz po tym jak gdzieś zainstalujesz `.app`

### 10.6-10.8

Aby zainstalować narzędzia prosto z pliku binarnego, użyj tej [dystrybucji](https://www.haskell.org/platform/download/2014.2.0.0/ghc-7.8.3-x86_64-apple-darwin-r3.tar.bz2)

## Windows

## Inne dystrybucje Linuxa

Sciągnij oraz zainstaluj najnowsze pliki binarne :

- [GHC](http://www.haskell.org/ghc/).

- [Cabal](https://www.haskell.org/cabal/download.html).

# Podstawowe kursy (poradniki??)

## Yorgey's cis194 course

> Najlepiej tutaj zacząć swoją przygode z Haskellem, jest to podstawywe wejscie w świat Haskella (?)

Dostępne [online](http://www.seas.upenn.edu/~cis194/spring13/lectures.html).

Kurs [Brent Yorgey](https://byorgey.wordpress.com) jest najlepszy jaki dotychczas znalazłem. Jest to wartościowy kurs który nie tylko pozwoli Ci na poznanie podstaw Haskella ale także pozowli Ci zrozumiec parser.

Istnieje tylko jedna dlaczego nie powinieneś zacząć od cis194, tylko dlatego jeśli nie jesteś programistą lub jesteś mało doświadczony. Wtedy zacznij od [książki](http://www.haskellcraft.com/craft3e/Home.html) a nastepnie możesz powoli przechodzić do cis194.

---

## Kurs NICTA

> Ten kurs polecam przerobić zaraz po kursie `Yorgey cis194`

Dostępne na [github](https://github.com/NICTA/course).

Ten kurs wzmocni twoją wiedze oraz da Ci mozliwość zaprogramowania abstrakcji która została opisana w cis194, to co jest opisane w tym kursie jest *krytyczne* aby być biegłym w użyciu Funktorów/Monad itd. w Haskellu

---

## Kurs dopełniający cs240h

> Zawiera wiecej materiałów o poziomie średnio-zaawansowanym.

Dostępne [na stronie](http://www.scs.stanford.edu/14sp-cs240h/).

Kurs [Bryan O'Sullivan](https://github.com/bos), jest to kurs który używał do nauki w Stanford. Jeśli nie wiesz kto to jest, weź połowe bibliotek do Haskella a zobaczysz ze połowa z tych bibliotek ma jego imię i nazwisko.

---

## Referencje do materiałów

[Learn You a Haskell for Great Good (LYAH)](http://learnyouahaskell.com) oraz
[Real World Haskell](http://book.realworldhaskell.org) są dostępne w sieci.

Polecam RWH jako referencja.

### Co dokładnie robi `<-` / `do` oraz porównywanie list ?

Super [artykuł](http://www.haskellforall.com/2014/10/how-to-desugar-haskell-code.html).

### List oraz foldy

- [Filmik który tłumaczy listy oraz foldy](http://vimeo.com/64673035).

### Do nauki typów

Bardzo pomocne aby zrozumieć `Funktory`, `Monady`, `Monoidy` oraz pozostałe typy. Dodatkowo można znaleźć informacje o teorii kategorii, stricte dla Haskella:

- [Typeclassopedia](http://www.haskell.org/haskellwiki/Typeclassopedia)

### Podstawowe wiadomości błędów w Haskellu

[Podstawowe wiadomości błędów](http://ics.p.lodz.pl/~stolarek/_media/pl:research:stolarek_understanding_basic_haskell_error_messages.pdf)

---

# Leniwe wartościowanie, bezpośrednie wartościowanie (?), rekurencja ogonowa

- [Książka](http://chimera.labs.oreilly.com/books/1230000000929/ch02.html) Marlow'a, na temat zrównoleglania i współbieżności. Jest to jedna z lepszych książek która wprowadza w świat leniwego wartościowania.

- [Więcej na temat leniwego wartościowania](http://augustss.blogspot.hu/2011/05/more-points-for-lazy-evaluation-in.html)

- [Oh my laziness!](http://alpmestan.com/posts/2013-10-02-oh-my-laziness.html)

- '[Czy haskell posiada leniwe wartościowanie?](http://stackoverflow.com/questions/13042353/does-haskell-have-tail-recursive-optimization)'

- Slajdy [Johan Tibell](https://github.com/tibbe) z prezentacji na temat [reasoning about laziness](http://www.slideshare.net/tibbe/reasoning-about-laziness).

## Demo

```haskell
let a = 1 : a -- guarded recursion, (:) is lazy and can be pattern matched.
let (v : _) = a
> v
1
> head a -- head a == v
1

let a = 1 * a -- not guarded, (*) is strict
> a
*** Exception: <<loop>>
```

# IO

- [Kolejność wywoływania oraz tokeny](https://www.fpcomplete.com/user/snoyberg/general-haskell/advanced/evaluation-order-and-state-tokens)

- [Unraveling the mystery of the IO monad](http://blog.ezyang.com/2011/05/unraveling-the-mystery-of-the-io-monad/).

- [First class "statements"](http://blog.jle.im/entry/first-class-statements).

- [Haddocks for System.IO.Unsafe.unsafePerformIO](http://hackage.haskell.org/package/base-4.7.0.1/docs/System-IO-Unsafe.html#v:unsafePerformIO)
  Read the docs and note implementation of unsafeDupablePerformIO

 Comment from Reddit thread by `glaebhoerl`

> Interesting side note: GHC needs to hide the state token representation behind
> an abstract IO type because the state token must always be used linearly (not
> duplicated or dropped), but the type system can't enforce this. Clean, another
> lazy Haskell-like language, has uniqueness types (which are like linear types
> and possibly different in ways I'm not aware of), and they expose the
> World-passing directly and provide a (non-abstract) IO monad only for
> convenience.

# Monady oraz transformaty modan

> Nie zaczynaj tej sekcji dopóki nie zrozumiesz typów klas, monoidów, funktorów oraz
>

Spróbuj zaimplementować standardowe biblioteki oparte o monady (List, Maybe, Cont, Error, Reader, Writer, State ), pozwoli Ci to bardziej zrozumieć monady. Następnie możesz zaimplementować interpreter [Monad Transformers Step by Step](http://www.cs.virginia.edu/~wh5a/personal/Transformers.pdf).

Writing many interpreters by just changing the monad to change the semantics can
help convey what's going on.

- [This talk](https://vimeo.com/73648150) by Tony excellently motivates monad
  transformers, [the slides](https://dl.dropboxusercontent.com/u/7810909/talks/monad-transformers/cbaa991e0eb49224eb286c1e418e2b9828e1fb21/monad-transformers.pdf).

Dodatkowo możesz zaimplementować `Control.Monad`. Funkcje takie jak `mapM` lub `sequence` to dobre przykłady do przećwiczenia generycznych mond.

Kurs NICTA może być pomocny przy implementowaniu od nowa wcześniejszych funkcji. Ponadto pozwoli Ci to na pisanie swoich własnych Applicative(?)

Credits:

- Reddit comment by htmltyp and Crandom [here](http://www.reddit.com/r/haskell/comments/29eke6/basic_program_ideas_for_learning_about_monads/cik5aj6).

- Reddit comment by jozefg [here](http://www.reddit.com/r/haskell/comments/29eke6/basic_program_ideas_for_learning_about_monads/cik5trg).

## Transformaty monad

- [A gentle introduction to Monad Transformers](https://github.com/kqr/gists/blob/master/articles/gentle-introduction-monad-transformers.md).

- [Monad transformers step-by-step](http://www.cs.virginia.edu/~wh5a/personal/Transformers.pdf) (warning, code out of date).

# Testowanie, testy, specs

- This [tutorial](https://github.com/kazu-yamamoto/unit-test-example/blob/master/markdown/en/tutorial.md) by Kazu Yamamoto is fantastic.

- [Simple-Conduit](https://github.com/jwiegley/simple-conduit): Good simple
  library for learning how streaming IO works in general, knowledge
  transferrable to libraries like Pipes and Conduit

# Parsowanie w Haskellu

- Parser combinator [tutorial](https://github.com/JakeWheat/intro_to_parsing)
  for Haskell using Parsec

- [Writing your own micro-Parsec](http://olenhad.me/articles/monadic-parsers/)

## Parsowanie oraz generowanie JSON

Aeson is the standard [JSON](https://json.org) parsing solution in
haskell. Available from [hackage](https://hackage.haskell.org/package/aeson) and
[github](https://github.com/bos/aeson).

- [Parsing JSON using Aeson](http://blog.raynes.me/blog/2012/11/27/easy-json-parsing-in-haskell-with-aeson/)

- [Aeson and user created types](http://bitemyapp.com/posts/2014-04-11-aeson-and-user-created-types.html)

- [Parsing non-deterministic data with aeson and sum types](http://bitemyapp.com/posts/2014-04-17-parsing-nondeterministic-data-with-aeson-and-sum-types.html)

- [Aeson tutorial](https://www.fpcomplete.com/school/starting-with-haskell/libraries-and-frameworks/text-manipulation/json)

# Algorytmy grafowe oraz struktury danych

- The [fgl package](https://hackage.haskell.org/package/fgl) particularly the
  purely functional shortest path [algos](http://hackage.haskell.org/package/fgl-5.4.2.2/docs/Data-Graph-Inductive-Query-SP.html).

- [Inductive graphs and Functional Graph Algorithms](http://web.engr.oregonstate.edu/~erwig/papers/abstracts.html#JFP01).

- [FGL/Haskell - A Functional Graph Library](http://web.engr.oregonstate.edu/~erwig/fgl/haskell/old/fgl0103.pdf).

- [Data.Graph source from Containers package](http://hackage.haskell.org/package/containers-0.5.5.1/docs/Data-Graph.html).

- The [graphs package](https://hackage.haskell.org/package/graphs).

- [SO question about PHOAS](http://stackoverflow.com/questions/24369954/separate-positive-and-negative-occurrences-of-phoas-variables-in-presence-of-rec)

- [PHOAS for free](https://www.fpcomplete.com/user/edwardk/phoas).

- [Tying the Knot](http://www.haskell.org/haskellwiki/Tying_the_Knot).

- [Hackage: dag](https://hackage.haskell.org/package/dag).

# Środowiska programistyczne

## Emacs

- [Alejandro Serras's tutorial](https://github.com/serras/emacs-haskell-tutorial/blob/master/tutorial.md)

- [My dotfiles](https://github.com/bitemyapp/dotfiles/)

- [Chris Done's emacs config](https://github.com/chrisdone/chrisdone-emacs)

## Vim

- [Vim page on haskellwiki](http://www.haskell.org/haskellwiki/Vim)

- [Haskell-vim-now](https://github.com/begriffs/haskell-vim-now)

- [A vim+haskell workflow](http://www.stephendiehl.com/posts/vim_haskell.html)

- [GHC-Mod](https://github.com/kazu-yamamoto/ghc-mod)

- [GHC-Mod vim plugin](https://github.com/eagletmt/ghcmod-vim)

- [Hindent](https://github.com/chrisdone/hindent)

## Sublime Text

- [SublimeHaskell](https://github.com/SublimeHaskell/SublimeHaskell)

# FAQ oraz jak pracować z Cabalem

## Super seria FAQ

In addition to being an amazing guide for all kinds of things such as GADTs,
this also covers some useful basics for Cabal

- [What I wish I knew when learning Haskell](http://dev.stephendiehl.com/hask/)
  also on github [here](https://github.com/sdiehl/wiwinwlh).

## Poradnik do Cabala

Cabal Hell was a problem for Haskell users before the introduction of
sandboxes. Installing outside of a sandbox will install into your user
package-db. This is *not* a good idea except for foundational packages like
Cabal, alex, and happy. Nothing else should be installed in the user or global
package-dbs unless you know what you're doing.

Some best practices for avoiding cabal hell are available
[here](http://softwaresimply.blogspot.com/2014/07/haskell-best-practices-for-avoiding.html).

To experiment with a package or start a project, begin by doing
`cabal sandbox init` in a new directory.

Put briefly:

- Always use sandboxes for installing new packages, building new or existing
  projects, or starting experiments

- Use `cabal repl` to start a project-scoped ghci instance

The sandbox-based approach I suggest should avoid package-dependency problems,
but it's incompatible with the way the Haskell Platform provides pre-built
packages. If you're still learning Haskell and don't understand how ghc-pkg and
Cabal work, *avoid platform* and instead use the install instructions earlier in
the guide.

## Stackage

For any users (usually Yesod users) that have build problems, consider Stackage.

- A good summary of Stackage is
  [here](https://www.fpcomplete.com/blog/2014/05/stackage-server).

In the author's opinion, Stackage is usually more useful than `cabal freeze`.

# Hoogle and Haddock

## Przeszukowanie kodu po sygnaturze

The [Hoogle search engine](http://www.haskell.org/hoogle/) can search by type.

For example, look at the search results for `(a -> b) -> [a] -> [b]`
[here](http://www.haskell.org/hoogle/?hoogle=%28a+-%3E+b%29+-%3E+%5ba%5d+-%3E+%5bb%5d).

Also hosted by fpcomplete [here](https://www.fpcomplete.com/hoogle).

Also [Hayoo](http://holumbus.fh-wedel.de/hayoo/hayoo.html) (which has all of
hackage enabled for search by default).

## Postaw lokalną instancje Hoogle

Take a look [here](https://gist.github.com/bitemyapp/3e6a015760775e0679bf).

## Haddock

1. [Fix your hackage documentation](http://fuuzetsu.co.uk/blog/posts/2014-01-06-Fix-your-Hackage-documentation.html)

2. [Hackage documentation v2](http://fuuzetsu.co.uk/blog/posts/2014-01-06-Hackage-documentation-v2.html)

Note that these posts are *slightly out of date*: for example, now Hackage sports
shiny new info with documentation info and build status.

## Co tak naprawde potrzebujesz wiedzieć ?

Note that these posts are *slightly out of date*: for example, now Hackage sports
shiny new info with documentation info and build status.

## What you really need to know

In order to have haddocks include documentation for related packages, you have
to set `documentation: True` in your `~/.cabal/config`. If it was left on the
default (`False`) or set to `False`, you'll have to delete all your packages and
reinstall before generating haddocks.

The other thing to keep in mind is that due to the way the `$pkg` parameter gets
interpolated *by* cabal, not by you, the `html-location` and `content-location`
parameters *must be in single quotes* and entered into a shell or contained in a
shell script. They will not work in a Makefile, because it will think they are
Make variables!

```bash
#! /usr/bin/env sh

# You can write it one one line by skipping the backslashes
cabal haddock --hoogle --hyperlink-source                       \
 --html-location='http://hackage.haskell.org/package/$pkg/docs' \
 --contents-location='http://hackage.haskell.org/package/$pkg'
```

# TravisCI

Jeśli jesteś wielkim fanem [TravisCI](https://travis-ci.org) tak jak ja, wtedy polecam Ci abyś zajrzał na [dokumentacje, multi-ghc-travis](https://github.com/hvr/multi-ghc-travis) pomoże Ci to skonfigurować `travis.yml` dla twoich projektów w Haskellu

# Frontend/JavaScript

Polecam głównie trzy pozycje do wyboru :

* [Haste](http://haste-lang.org/) a Haskell to JavaScript compiler
  - The [compiler](https://github.com/valderman/haste-compiler) on github.
  - An excellent
    [demo](http://www.airpair.com/haskell/posts/haskell-tutorial-introduction-to-web-apps)
    of Haste with an example project.

* [GHCJS](https://github.com/ghcjs/ghcjs)
  - [GHCJS Introduction](http://weblog.luite.com/wordpress/?p=14)
  - [Functional Reactive Web Interfaces with GHCJS and Sodium](http://weblog.luite.com/wordpress/?p=127)
  - [Writing Atom plugins in Haskell using ghcjs ](http://edsko.net/2015/02/14/atom-haskell/)

* [PureScript](http://www.purescript.org/)
  - Not strictly Haskell like Haste and GHCJS, but a popular choice among
    Haskellers
  - Written in and inspired by haskell
  - Try purescript in you browser [here](http://try.purescript.org/)
  - Great guide for [getting started](http://www.christopherbiscardi.com/2014/06/22/getting-started-with-purescript/)

## Który język do frontendu ?

GHCJS i Haste oba są w pełni na podstawie Haskella jednak GHCJS jest kompatybilny z większością bibliotek, w przeciwieństwie do Haste który jest kompatybilny z miejszą ilością bibliotek. PureScript w ogóle nie jest na podstawie Haskella, więc bezpośrednie dzielenie kodu z backendem w tym przypadku nie zadziała!

GHCJS jest najcięższą z bibliotek, waży około 100kb. Haste oraz PureScript tutaj wygrywają.

PureScript ma najlepsze narzędzia takie jak (gulp/grunt/bower), natomiast GHCJS oraz Haste lepiej integrują się z narzędziami Haskella (Cabal).

Wszystie trzy powyższe pozycje są dobre, i zadziałają na większości projektów.

# Jeszcze więcej na temat laziness, NF, WHNF

- [Notes on lambda calculus](https://vec.io/posts/notes-on-lambda-calculus).

## Publikacje naukowe na temat lazy lambda calculi

- [A call by need lambda calculus](http://homepages.inf.ed.ac.uk/wadler/topics/call-by-need.html#need-journal).

- [Demonstrating Lambda Calculus Reduction](http://www.itu.dk/~sestoft/papers/sestoft-lamreduce.pdf)

- [The lazy lambda calculus](http://www.cs.ox.ac.uk/files/293/lazy.pdf).

- [Lazy evaluation of Haskell](http://www.vex.net/~trebla/haskell/lazy.xhtml)

# Równoległość/Współbieżność

- [Parallel and Concurrent Programming in Haskell](http://chimera.labs.oreilly.com/books/1230000000929). This
  book by Simon Marlow is probably the best I've ever read on the topics of
  Parallelism and Concurrency.

  - A thorough [walk-through](http://kukuruku.co/hub/haskell/haskell-testing-a-multithread-application)
  on testing & incremental development of a multi-threaded application in
  Haskell.

  - [Functional Reactive Programming](http://www.haskell.org/haskellwiki/Functional_Reactive_Programming)

  # Lenses and Prisms (? translate)

  Jeśli jesteś na tyle obeznany w Haskellu, zastanów się nad nauką lenses oraz prisms.

  Ludzie często zawyżają poziom trudności Lens. Każdy kto czuje się swobodnie przy Funktorach/Foldach/Traversable(?) (nawet tylko z pierwszym), może wykorzystać przewage lenses oraz prisms i uczynić swoje życie lepszym ;)

  Jeśli kiedykolwiek zrobileś coś takiego : `(fmap . fmap)` w tym momencie "lensing" w swojej głowie.

  Polecam nastepujące twa poradniki :

  - [A little lens starter tutorial](https://www.fpcomplete.com/school/to-infinity-and-beyond/pick-of-the-week/a-little-lens-starter-tutorial)

- [Lens: Lenses, Folds and Traversals](https://github.com/ekmett/lens#lens-lenses-folds-and-traversals)

Look here for more information: [Lens package on hackage](http://hackage.haskell.org/package/lens).

# Schemat rekurencji (?)

Some of the crazy \*-morphism words you've heard are actually about
recursion. NB - before tackling this material you should know how to implement
foldr for lists and at least one other data structure, such as a tree. (folds
are catamorphisms) Knowing how to implement an unfold (anamorphism) for the same
will round things out a bit.

Poniżej znajdziecie materiały dla traversable oraz foldable.

- [An introduction to recursion schemes](http://patrickthomson.ghost.io/an-introduction-to-recursion-schemes/)

- [Don't fear the cat](http://fho.f12n.de/posts/2014-05-07-dont-fear-the-cat.html) -
  Good demonstration of how hylomorphism is the composition of cata and ana.

- [Recursion Schemes](http://comonad.com/reader/2009/recursion-schemes/) - This
  field guide is excellent.

- [Functional Programming with Bananas, Lenses, Envelopes and Barbed Wire](http://eprints.eemcs.utwente.nl/7281/01/db-utwente-40501F46.pdf)

- [Catamorphisms](https://www.fpcomplete.com/user/edwardk/recursion-schemes/catamorphisms)

# GHC Core i podkręcanie wydajności

- [Write Haskell as Fast as C](write_haskell_as_fast_as_c.md)

- [GHC Wiki: CoreSyn Type](https://ghc.haskell.org/trac/ghc/wiki/Commentary/Compiler/CoreSynType).

- [Hackage: GHC Core](https://hackage.haskell.org/package/ghc-core).

- [SO Question: Reading GHC Core](http://stackoverflow.com/questions/6121146/reading-ghc-core).

- [Haskell as fast as C](http://donsbot.wordpress.com/2008/06/04/haskell-as-fast-as-c-working-at-a-high-altitude-for-low-level-performance/).

- [Real World Haskell, Chapter 25: Profiling and Optimizations](http://book.realworldhaskell.org/read/profiling-and-optimization.html).

# Typy oraz teoria kategorii

> *Nie* jest to coś co musisz przerabiać aby zrozumieć Haskella, tylko dla zainteresowanych!

Jeśli chcesz śledzić i pouczyć się więcej na temat typów i teorii kategorii:

- [Catster's Guide](http://byorgey.wordpress.com/2014/01/14/catsters-guide/) and
  [Catster's Guide 2](http://byorgey.wordpress.com/catsters-guide-2/)

- The [haskell wikibook](http://en.wikibooks.org/wiki/Haskell/Category_theory)
  has nice diagrams

- [Category Theory](http://www.haskell.org/haskellwiki/Category_theory) on
  haskellwiki, also has good links to other resources

- [Categories from scratch](http://science.raphael.poss.name/categories-from-scratch.html), Includes some practical examples.

- Pierce's [Great Works in PL](http://www.cis.upenn.edu/~bcpierce/courses/670Fall04/GreatWorksInPL.shtml) list.

## Książki

- [Quora Question: What is the best textbook for category theory?](http://www.quora.com/Category-Theory/What-is-the-best-textbook-for-Category-theory?share=1) Kmett's recommendations

- [Awodey](http://ukcatalogue.oup.com/product/9780199237180.do) and
  [MacLane](http://www.amazon.com/Categories-Working-Mathematician-Graduate-Mathematics/dp/0387984038). The standard textbooks on category theory.

- [Harper's Practical Foundations for Programming Languages](http://www.cs.cmu.edu/~rwh/plbook/book.pdf) is the best PL focused intro to type theory I've read.

- [Type theory and Functional Programming](http://www.cs.kent.ac.uk/people/staff/sjt/TTFP/).

## Stephen's Nifty "How to get to monad" posts

- [Adjunctions](http://www.stephendiehl.com/posts/adjunctions.html).

- [Monads](http://www.stephendiehl.com/posts/monads.html).

# Inne fajne zagadnienia

## Parametricity, ad-hoc vs. parametric polymorphism, free theorems

- [Parametricity](tony_parametricity.pdf).

- [TeX sources](https://github.com/tonymorris/parametricity/) for the
  above talk.

- [Making ad-hoc polymorphism less ad-hoc](http://swizec.com/blog/week-20-making-ad-hoc-polymorphism-less-ad-hoc/swizec/6564).

- [Theorems for Free!](http://ttic.uchicago.edu/~dreyer/course/papers/wadler.pdf).

## Initial and Final, DSLs, Finally Tagless

- [Final Encodings, Part 1: A Quick Demonstration](http://creativelad.wordpress.com/2013/11/28/final-encodings-part-1-a-quick-demonstration/).

- [Transforming Polymorphic Values](http://martijn.van.steenbergen.nl/journal/2009/10/18/transforming-polymorphic-values/).

- [GADTs in Haskell 98](http://martijn.van.steenbergen.nl/journal/2009/11/12/gadts-in-haskell-98/).

- [Typed Tagless-Final Linear Lambda Calculus](https://www.fpcomplete.com/user/mutjida/typed-tagless-final-linear-lambda-calculus).

- [Typed tagless-final interpretations: Lecture notes](http://okmij.org/ftp/tagless-final/course/course.html).

- [Typed Tagless Final Interpreters](http://okmij.org/ftp/tagless-final/course/lecture.pdf).

- [The dog that didn't bark](http://existentialtype.wordpress.com/2011/03/21/the-dog-that-didnt-bark/) less specifically relevant but interesting.

## Comonads

- [Comonads in Haskell](https://speakerdeck.com/dmoverton/comonads-in-haskell).

- [SO question: Can a Monad be a Comonad](http://stackoverflow.com/questions/16551734/can-a-monad-be-a-comonad).

## Yoneda / CoYoneda

- [SO question: Step-by-step explanation of coyoneda](http://stackoverflow.com/questions/24000465/step-by-step-deep-explain-the-power-of-coyoneda-preferably-in-scala-throu).

- Free monads for Less, a sequence of three articles by Edward Kmett
  * [Part 1: Codensity](http://comonad.com/reader/2011/free-monads-for-less/).
  * [Part 2: Yoneda](http://comonad.com/reader/2011/free-monads-for-less-2/).
  * [Part 3: Yielding IO](http://comonad.com/reader/2011/free-monads-for-less-3/).

## Propositions vs. Judgments (computation)

- [StackExchange question: What is the difference between propositions and judgements](http://cstheory.stackexchange.com/questions/9826/what-is-the-difference-between-propositions-and-judgments).

- [Lecture notes from a short, three lecture course](http://www.ae-info.org/attach/User/Martin-L%C3%B6f_Per/OtherInformation/article.pdf)

# Dependent typing

- [Grokking sum types, value constructors, and type constructors](http://bitemyapp.com/posts/2014-04-05-grokking-sums-and-constructors.html) squint hard.

- [Lightweight Dependent-type Programming](http://okmij.org/ftp/Computation/lightweight-dependent-typing.html).

- [Idris programming language](http://www.idris-lang.org/).

# Statically linking binaries

- [Static linking](https://wiki.haskell.org/Web/Literature/Static_linking)

- [Static linking with GHC on Arch Linux](http://www.edofic.com/posts/2014-05-03-ghc-arch-static.html)

- [Statically linking Linux binaries for ARM & MIPS](http://stackoverflow.com/questions/14270177/ghc-statically-linking-linux-binaries-for-arm-mips-processors)

- [Statically link GMP using GHC and LLVM](http://stackoverflow.com/questions/10539857/statically-link-gmp-to-an-haskell-application-using-ghc-llvm)

# Extended Reading list

> Some are already included here

- [Essential Haskell Reading List](http://www.stephendiehl.com/posts/essential_haskell.html)

## Dialogues

> Hosted in this repository [here](dialogues.md).

These are actually pretty important and helpful. Look here for deep dives on a
variety of topics.

