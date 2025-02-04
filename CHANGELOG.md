# Documenter.jl changelog

## Version `v0.23.0`

* Documenter v0.23 requires Julia v1.0. ([#1015][github-1015])

* ![Enhancement][badge-enhancement] The logo image in the HTML output will now always point to the first page in the navigation menu (as opposed to `index.html`, which may or may not exist). When using pretty URLs, the `index.html` part now omitted from the logo link URL. ([#1005][github-1005])

* ![Enhancement][badge-enhancement] Minor changes to how doctesting errors are printed. ([#1028][github-1028])

## Version `v0.22.4`

* ![Bugfix][badge-bugfix] Documenter no longer crashes if the build includes doctests from docstrings that are defined in files that do not exist on the file system (e.g. if a Julia Base docstring is included when running a non-source Julia build). ([#1002][github-1002])

* ![Bugfix][badge-bugfix] URLs for files in the repository are now generated correctly when the repository is used as a Git submodule in another repository. ([#1000][github-1000], [#1004][github-1004])

* ![Bugfix][badge-bugfix] When checking for omitted docstrings, Documenter no longer gives "`Package.Package` missing" type false positives. ([#1009][github-1009])

* ![Bugfix][badge-bugfix] `makedocs` again exits with an error if `strict=true` and there is a doctest failure. ([#1003][github-1003], [#1014][github-1014])

## Version `v0.22.3`

* ![Bugfix][badge-bugfix] Fixed filepaths for images included in the .tex file for PDF output on Windows. ([#999][github-999])

## Version `v0.22.2`

* ![Bugfix][badge-bugfix] Error reporting for meta-blocks now handles missing files gracefully instead of throwing. ([#996][github-996])

* ![Enhancement][badge-enhancement] The `sitename` keyword argument to `deploydocs`, which is required for the default HTML output, is now properly documented. ([#995][github-995])

## Version `v0.22.1`

* ![Bugfix][badge-bugfix] Fixed a world-age related bug in doctests. ([#994][github-994])

## Version `v0.22.0`

* ![Deprecation][badge-deprecation] ![Enhancement][badge-enhancement] The `assets` and `analytics` arguments to `makedocs` have been deprecated in favor of the corresponding arguments of the `Documenter.HTML` format plugin. ([#953][github-953])

  **For upgrading:** pass the corresponding arguments with the `Documenter.HTML` plugin instead. E.g. instead of

  ```
  makedocs(
      assets = ..., analytics = ...,
      ...
  )
  ```

  you should have

  ```
  makedocs(
      format = Documenter.HTML(assets = ..., analytics = ...),
      ...
  )
  ```

  _**Note:** It is technically possible to specify the same argument twice with different values by passing both variants. In that case the value passed to `makedocs` takes precedence._

* ![Enhancement][badge-enhancement] Documentation is no longer deployed on Travis CI cron jobs. ([#917][github-917])

* ![Enhancement][badge-enhancement] Log messages from failed `@meta`, `@docs`, `@autodocs`,
  `@eval`, `@example` and `@setup` blocks now include information about the source location
  of the block. ([#929][github-929])

* ![Enhancement][badge-enhancement] Docstrings from `@docs`-blocks are now included in the
  rendered docs even if some part(s) of the block failed. ([#928][github-928], [#935][github-935])

* ![Enhancement][badge-enhancement] The Markdown and LaTeX output writers can now handle multimedia
  output, such as images, from `@example` blocks. All the writers now also handle `text/markdown`
  output, which is preferred over `text/plain` if available. ([#938][github-938], [#948][github-948])

* ![Enhancement][badge-enhancement] The HTML output now also supports SVG, WebP, GIF and JPEG logos. ([#953][github-953])

* ![Enhancement][badge-enhancement] Reporting of failed doctests are now using the logging
  system to be consistent with the rest of Documenter's output. ([#958][github-958])

* ![Enhancement][badge-enhancement] The construction of the search index in the HTML output has been refactored to make it easier to use with other search backends in the future. The structure of the generated search index has also been modified, which can yield slightly different search results. Documenter now depends on the lightweight [JSON.jl][json-jl] package. ([#966][github-966])

* ![Enhancement][badge-enhancement] Docstrings that begin with an indented code block (such as a function signature) now have that block highlighted as Julia code by default.
  This behaviour can be disabled by passing `highlightsig=false` to `makedocs`. ([#980][github-980])

* ![Bugfix][badge-bugfix] Paths in `include` calls in `@eval`, `@example`, `@repl` and `jldoctest`
  blocks are now interpreted to be relative `pwd`, which is set to the output directory of the
  resulting file. ([#941][github-941])

* ![Bugfix][badge-bugfix] `deploydocs` and `git_push` now support non-github repos correctly and work when the `.ssh` directory does not already exist or the working directory contains spaces. ([#971][github-971])

* ![Bugfix][badge-bugfix] Tables now honor column alignment in the HTML output. If a column does not explicitly specify its alignment, the parser defaults to it being right-aligned, whereas previously all cells were left-aligned. ([#511][github-511], [#989][github-989])

* ![Bugfix][badge-bugfix] Code lines ending with `# hide` are now properly hidden for CRLF inputs. ([#991][github-991])

## Version `v0.21.5`

* ![Bugfix][badge-bugfix] Deprecation warnings for `format` now get printed correctly when multiple formats are passed as a `Vector`. ([#967][github-967])

## Version `v0.21.4`

* ![Bugfix][badge-bugfix] A bug in `jldoctest`-blocks that, in rare cases, resulted in
  wrong output has been fixed. ([#959][github-959], [#960][github-960])

## Version `v0.21.3`

* ![Security][badge-security] The lunr.js and lodash JavaScript dependencies have been updated to their latest patch versions (from 2.3.1 to 2.3.5 and 4.17.4 to 4.17.11, respectively).
  This is in response to a vulnerability in lodash <4.17.11 ([CVE-2018-16487](https://nvd.nist.gov/vuln/detail/CVE-2018-16487)). ([#946][github-946])

## Version `v0.21.2`

* ![Bugfix][badge-bugfix] `linkcheck` now handles servers that do not support `HEAD` requests
  and properly checks for status codes of FTP responses. ([#934][github-934])

## Version `v0.21.1`

* ![Bugfix][badge-bugfix] `@repl` blocks now work correctly together with quoted
  expressions. ([#923][github-923], [#926][github-926])

* ![Bugfix][badge-bugfix] `@example`, `@repl` and `@eval` blocks now handle reserved words,
  e.g. `try`/`catch`, correctly. ([#886][github-886], [#927][github-927])

## Version `v0.21.0`

* ![Deprecation][badge-deprecation] ![Enhancement][badge-enhancement] The symbol values to the `format` argument of `makedocs` (`:html`, `:markdown`, `:latex`) have been deprecated in favor of the `Documenter.HTML`, `Markdown` and `LaTeX`
  objects. The `Markdown` and `LaTeX` types are exported from the [DocumenterMarkdown][documentermarkdown] and [DocumenterLaTeX][documenterlatex] packages,
  respectively. HTML output is still the default. ([#891][github-891])

  **For upgrading:** If you don't specify `format` (i.e. you rely on the default) you don't have to do anything.
  Otherwise update calls to `makedocs` to use struct instances instead of symbols, e.g.

  ```
  makedocs(
      format = :markdown
  )
  ```

  should be changed to

  ```
  using DocumenterMarkdown
  makedocs(
      format = Markdown()
  )
  ```

* ![Deprecation][badge-deprecation] ![Enhancement][badge-enhancement] The `html_prettyurls`, `html_canonical`, `html_disable_git` and `html_edit_branch` arguments to `makedocs` have been deprecated in favor of the corresponding arguments of the `Documenter.HTML` format plugin. ([#864][github-864], [#891][github-891])

  **For upgrading:** pass the corresponding arguments with the `Documenter.HTML` plugin instead. E.g. instead of

  ```
  makedocs(
      html_prettyurls = ..., html_canonical = ...,
      ...
  )
  ```

  you should have

  ```
  makedocs(
      format = Documenter.HTML(prettyurls = ..., canonical = ...),
      ...
  )
  ```

  _**Note:** It is technically possible to specify the same argument twice with different values by passing both variants. In that case the value to the deprecated `html_*` variant takes precedence._

* ![Feature][badge-feature] Packages extending Documenter can now define subtypes of `Documenter.Plugin`,
  which can be passed to `makedocs` as positional arguments to pass options to the extensions. ([#864][github-864])

* ![Feature][badge-feature] `@autodocs` blocks now support the `Filter` keyword, which allows passing a user-defined function that will filter the methods spliced in by the at-autodocs block. ([#885][github-885])

* ![Enhancement][badge-enhancement] `linkcheck` now supports checking URLs using the FTP protocol. ([#879][github-879])

* ![Enhancement][badge-enhancement] Build output logging has been improved and switched to the logging macros from `Base`. ([#876][github-876])

* ![Enhancement][badge-enhancement] The default `documenter.sty` LaTeX preamble now include `\usepackage{graphicx}`. ([#898][github-898])

* ![Enhancement][badge-enhancement] `deploydocs` is now more helpful when it fails to interpret `DOCUMENTER_KEY`. It now also uses the `BatchMode` SSH option and throws an error instead of asking for a passphrase and timing out the Travis build when `DOCUMENTER_KEY` is broken. ([#697][github-697], [#907][github-907])

* ![Enhancement][badge-enhancement] `deploydocs` now have a `forcepush` keyword argument that can be used to
  force-push the built documentation instead of adding a new commit. ([#905][github-905])

## Version `v0.20.0`

* Documenter v0.20 requires at least Julia v0.7. ([#795][github-795])

* ![BREAKING][badge-breaking] Documentation deployment via the `deploydocs` function has changed considerably.

  - The user-facing directories (URLs) of different versions and what gets displayed in the version selector have changed. By default, Documenter now creates the `stable/` directory (as before) and a directory for every minor version (`vX.Y/`). The `release-X.Y` directories are no longer created. ([#706][github-706], [#813][github-813], [#817][github-817])

    Technically, Documenter now deploys actual files only to `dev/` and `vX.Y.Z/` directories. The directories (URLs) that change from version to version (e.g. `latest/`, `vX.Y`) are implemented as symlinks on the `gh-pages` branch.

    The version selector will only display `vX.Y/`, `stable/` and `dev/` directories by default. This behavior can be customized with the `versions` keyword of `deploydocs`.

  - Documentation from the development branch (e.g. `master`) now deploys to `dev/` by default (instead of `latest/`). This can be customized with the `devurl` keyword. ([#802][github-802])

  - The `latest` keyword to `deploydocs` has been deprecated and renamed to `devbranch`. ([#802][github-802])

  - The `julia` and `osname` keywords to `deploydocs` are now deprecated. ([#816][github-816])

  - The default values of the `target`, `deps` and `make` keywords to `deploydocs` have been changed. See the default format change below for more information. ([#826][github-826])

  **For upgrading:**

  - If you are using the `latest` keyword, then just use `devbranch` with the same value instead.

  - Update links that point to `latest/` to point to `dev/` instead (e.g. in the README).

  - Remove any links to the `release-X.Y` branches and remove the directories from your `gh-pages` branch.

  - The operating system and Julia version should be specified in the Travis build stage configuration (via `julia:` and `os:` options, see "Hosting Documentation" in the manual for more details) or by checking the `TRAVIS_JULIA_VERSION` and `TRAVIS_OS_NAME` environment variables in `make.jl` yourself.

* ![BREAKING][badge-breaking] `makedocs` will now build Documenter's native HTML output by default and `deploydocs`' defaults now assume the HTML output. ([#826][github-826])

  - The default value of the `format` keyword of `makedocs` has been changed to `:html`.

  - The default value of the `target` keyword to `deploydocs` has been changed to `"build"`.

  - The default value of the `make` and `deps` keywords to `deploydocs` have been changed to `nothing`.

  **For upgrading:** If you are relying on the Markdown/MkDocs output, you now need to:

  - In `makedocs`, explicitly set `format = :markdown`

  - In `deploydocs`, explicitly set

    ```julia
    target = "site"
    deps = Deps.pip("pygments", "mkdocs")
    make = () -> run(`mkdocs build`)
    ```

  - Explicitly import `DocumenterMarkdown` in `make.jl`. See the `MarkdownWriter` deprecation below.

  If you already specify any of the changed keywords, then you do not need to make any changes to those keywords you already set.

  However, if you are setting any of the values to the new defaults (e.g. when you are already using the HTML output), you may now rely on the new defaults.

* ![Deprecation][badge-deprecation] The Markdown/MkDocs (`format = :markdown`) and PDF/LaTeX (`format = :latex`) outputs now require an external package to be loaded ([DocumenterMarkdown](https://github.com/JuliaDocs/DocumenterMarkdown.jl) and [DocumenterLaTeX](https://github.com/JuliaDocs/DocumenterLaTeX.jl), respectively). ([#833][github-833])

  **For upgrading:** Make sure that the respective extra package is installed and then just add `using DocumenterMarkdown` or `using DocumenterLaTeX` to `make.jl`.

* ![BREAKING][badge-breaking] "Pretty URLs" are enabled by default now for the HTML output. The default value of the `html_prettyurls` has been changed to `true`.

  For a page `foo/page.md` Documenter now generates `foo/page/index.html`, instead of `foo/page.html`.
  On GitHub pages deployments it means that your URLs look like  `foo/page/` instead of `foo/page.html`.

  For local builds you should explicitly set `html_prettyurls = false`.

  **For upgrading:** If you wish to retain the old behavior, set `html_prettyurls = false` in `makedocs`. If you already set `html_prettyurls`, you do not need to change anything.

* ![BREAKING][badge-breaking] The `Travis.genkeys` and `Documenter.generate` functions have been moved to a separate [DocumenterTools.jl package](https://github.com/JuliaDocs/DocumenterTools.jl). ([#789][github-789])

* ![Enhancement][badge-enhancement] If Documenter is not able to determine which Git hosting service is being used to host the source, the "Edit on XXX" links become "Edit source" with a generic icon. ([#804][github-804])

* ![Enhancement][badge-enhancement] The at-blocks now support `MIME"text/html"` rendering of objects (e.g. for interactive plots). I.e. if a type has `show(io, ::MIME"text/html", x)` defined, Documenter now uses that when rendering the objects in the document. ([#764][github-764])

* ![Enhancement][badge-enhancement] Enhancements to the sidebar. When loading a page, the sidebar will jump to the current page now. Also, the scrollbar in WebKit-based browsers look less intrusive now. ([#792][github-792], [#854][github-854], [#863][github-863])

* ![Enhancement][badge-enhancement] Minor style enhancements to admonitions. ([#841][github-841])

* ![Bugfix][badge-bugfix] The at-blocks that execute code can now handle `include` statements. ([#793][github-793], [#794][github-794])

* ![Bugfix][badge-bugfix] At-docs blocks no longer give an error when containing empty lines. ([#823][github-823], [#824][github-824])

[github-511]: https://github.com/JuliaDocs/Documenter.jl/pull/511
[github-697]: https://github.com/JuliaDocs/Documenter.jl/pull/697
[github-706]: https://github.com/JuliaDocs/Documenter.jl/pull/706
[github-764]: https://github.com/JuliaDocs/Documenter.jl/pull/764
[github-789]: https://github.com/JuliaDocs/Documenter.jl/pull/789
[github-792]: https://github.com/JuliaDocs/Documenter.jl/pull/792
[github-793]: https://github.com/JuliaDocs/Documenter.jl/pull/793
[github-794]: https://github.com/JuliaDocs/Documenter.jl/pull/794
[github-795]: https://github.com/JuliaDocs/Documenter.jl/pull/795
[github-802]: https://github.com/JuliaDocs/Documenter.jl/pull/802
[github-804]: https://github.com/JuliaDocs/Documenter.jl/pull/804
[github-813]: https://github.com/JuliaDocs/Documenter.jl/pull/813
[github-816]: https://github.com/JuliaDocs/Documenter.jl/pull/816
[github-817]: https://github.com/JuliaDocs/Documenter.jl/pull/817
[github-823]: https://github.com/JuliaDocs/Documenter.jl/pull/823
[github-824]: https://github.com/JuliaDocs/Documenter.jl/pull/824
[github-826]: https://github.com/JuliaDocs/Documenter.jl/pull/826
[github-833]: https://github.com/JuliaDocs/Documenter.jl/pull/833
[github-841]: https://github.com/JuliaDocs/Documenter.jl/pull/841
[github-854]: https://github.com/JuliaDocs/Documenter.jl/pull/854
[github-863]: https://github.com/JuliaDocs/Documenter.jl/pull/863
[github-864]: https://github.com/JuliaDocs/Documenter.jl/pull/864
[github-876]: https://github.com/JuliaDocs/Documenter.jl/pull/876
[github-879]: https://github.com/JuliaDocs/Documenter.jl/pull/879
[github-885]: https://github.com/JuliaDocs/Documenter.jl/pull/885
[github-886]: https://github.com/JuliaDocs/Documenter.jl/pull/886
[github-891]: https://github.com/JuliaDocs/Documenter.jl/pull/891
[github-898]: https://github.com/JuliaDocs/Documenter.jl/pull/898
[github-905]: https://github.com/JuliaDocs/Documenter.jl/pull/905
[github-907]: https://github.com/JuliaDocs/Documenter.jl/pull/907
[github-917]: https://github.com/JuliaDocs/Documenter.jl/pull/917
[github-923]: https://github.com/JuliaDocs/Documenter.jl/pull/923
[github-926]: https://github.com/JuliaDocs/Documenter.jl/pull/926
[github-927]: https://github.com/JuliaDocs/Documenter.jl/pull/927
[github-928]: https://github.com/JuliaDocs/Documenter.jl/pull/928
[github-929]: https://github.com/JuliaDocs/Documenter.jl/pull/929
[github-934]: https://github.com/JuliaDocs/Documenter.jl/pull/934
[github-935]: https://github.com/JuliaDocs/Documenter.jl/pull/935
[github-938]: https://github.com/JuliaDocs/Documenter.jl/pull/938
[github-941]: https://github.com/JuliaDocs/Documenter.jl/pull/941
[github-946]: https://github.com/JuliaDocs/Documenter.jl/pull/946
[github-948]: https://github.com/JuliaDocs/Documenter.jl/pull/948
[github-953]: https://github.com/JuliaDocs/Documenter.jl/pull/953
[github-958]: https://github.com/JuliaDocs/Documenter.jl/pull/958
[github-959]: https://github.com/JuliaDocs/Documenter.jl/pull/959
[github-960]: https://github.com/JuliaDocs/Documenter.jl/pull/960
[github-966]: https://github.com/JuliaDocs/Documenter.jl/pull/966
[github-967]: https://github.com/JuliaDocs/Documenter.jl/pull/967
[github-971]: https://github.com/JuliaDocs/Documenter.jl/pull/971
[github-980]: https://github.com/JuliaDocs/Documenter.jl/pull/980
[github-989]: https://github.com/JuliaDocs/Documenter.jl/pull/989
[github-991]: https://github.com/JuliaDocs/Documenter.jl/pull/991
[github-994]: https://github.com/JuliaDocs/Documenter.jl/pull/994
[github-995]: https://github.com/JuliaDocs/Documenter.jl/pull/995
[github-996]: https://github.com/JuliaDocs/Documenter.jl/pull/996
[github-999]: https://github.com/JuliaDocs/Documenter.jl/pull/999
[github-1005]: https://github.com/JuliaDocs/Documenter.jl/pull/1005
[github-1000]: https://github.com/JuliaDocs/Documenter.jl/issues/1000
[github-1002]: https://github.com/JuliaDocs/Documenter.jl/pull/1002
[github-1003]: https://github.com/JuliaDocs/Documenter.jl/issues/1003
[github-1004]: https://github.com/JuliaDocs/Documenter.jl/pull/1004
[github-1009]: https://github.com/JuliaDocs/Documenter.jl/pull/1009
[github-1014]: https://github.com/JuliaDocs/Documenter.jl/pull/1014
[github-1015]: https://github.com/JuliaDocs/Documenter.jl/pull/1015
[github-1028]: https://github.com/JuliaDocs/Documenter.jl/pull/1028

[documenterlatex]: https://github.com/JuliaDocs/DocumenterLaTeX.jl
[documentermarkdown]: https://github.com/JuliaDocs/DocumenterMarkdown.jl
[json-jl]: https://github.com/JuliaIO/JSON.jl


[badge-breaking]: https://img.shields.io/badge/BREAKING-red.svg
[badge-deprecation]: https://img.shields.io/badge/deprecation-orange.svg
[badge-feature]: https://img.shields.io/badge/feature-green.svg
[badge-enhancement]: https://img.shields.io/badge/enhancement-blue.svg
[badge-bugfix]: https://img.shields.io/badge/bugfix-purple.svg
[badge-security]: https://img.shields.io/badge/security-black.svg

<!--
# Badges

![BREAKING][badge-breaking]
![Deprecation][badge-deprecation]
![Feature][badge-feature]
![Enhancement][badge-enhancement]
![Bugfix][badge-bugfix]
![Security][badge-security]
-->
