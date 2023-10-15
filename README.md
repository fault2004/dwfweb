# dwfweb.

<https://github.com/fault2004/dwfweb>
[(example website)](https://fault2004.github.io/dwfweb/)

My attempt at creating a *very bad* 18 line of code
markdown static website generator based on POSIX script, powered by smu.

[smu](https://github.com/Gottox/smu) is simple and minimal markup language
that convert markdown into HTML easily.

![dwarf](m/dwarf_fortress.png)

dwarf, from Dwarf Fortress (Video game)

## Features. (?)

* Using two template, loop, smu, sed, tr, cut and POSIX parameter substitution
* Title by filename of markdown files
* Generate menu and date
* Markdown supported by default and only
* POSIX-compliant

## Code.

The code itself.

		#!/bin/sh
		# dwfweb, static website generator, emelhnn @ 2022, MIT <https://github.com/emelhnn/dwfweb>
		[ ! -f smu/smu ] && (cd smu && make); [ -d o ] && rm -rf o; mkdir o; cp -r m o
		for pd in p/*; do
		p="${pd##*/}"; pe="${p%%.*}"
		pn="$(echo "$pe" | cut -c 1,1 | tr '[:lower:]' '[:upper:]')$(echo "$pe" | cut -c2-)"
		{
		    sed "s/TITLE/${pn}/g" header
		    for pl in p/*; do
		        P="${pl##*/}"; PE="${P%%.*}"
		        PN="$(echo "$PE" | cut -c 1,1 | tr '[:lower:]' '[:upper:]')$(echo "$PE" | cut -c2-)"
		        [ "$PE" != "index" ] && echo "<a id=menu_link href=${PE}.html>${PN}</a>"
		    done
		    echo "</div>"
		    smu/smu p/"$p"
		    sed "s/DATE/$(date)/g" footer
		} > o/"$pe".html
		done

## Running.

You need build tools to building smu from source, dwfweb will build smu for you.

		git clone https://github.com/emelhnn/dwfweb && cd dwfweb
		git submodule update --init
		./dwfweb

After that, generated website will be available in 'o' folder

## License.

dwfweb created by Chinathip Duanghoy (aka [fault2004](https://github.com/fault2004))
under the MIT License. 

smu created by [Enno T. Boland](https://github.com/Gottox)
under the MIT/X Consortium License. 
