OAIS Differ
===========

Using Markdown and GitHub to see how the OAIS has changed:

- [2002 v. 2012](https://github.com/anjackson/oais-differ/commit/4493459b922e61fa811d53caa9b40dd43eba2a9a)
- [2012 to 2024](https://github.com/anjackson/oais-differ/commit/80b90c307182ca7fda0f6cfec6187a61ca3b10ca)
 
(you'll have to click to make it load the large diff)

How This Was Done
-----------------

- Downloaded each version of the OAIS standard PDF
- Used [Docling](https://docling-project.github.io/docling/) to convert PDF to Markdown.
- Used an editor to normalise spaces `:%s/ +/ /g`
- **TODO** Strip repeated page headers (`## CCSDS RECOMMENDED PRACTICE FOR AN OAIS REFERENCE MODEL` and `## CCSDS HISTORICAL DOCUMENT`)
- **TODO** Strip 3+ multiple newlines down to two.
- Committed the results to git and pushed to GitHub.

The best arrangements for how to add them to Git were not clear.  I tried committing them as branches and as tags, and neither seemed to work that well. Partially because you're comparing commits, and these commits include the image files, which clutter up the difference view.  But also, when comparing branches, it seemed to struggle to compare them when there was a common history, but subsequent commits had been added (normalising spaces).

It wasn't clear to me why that wasn't working, so I just explicitly added each version to the `main` branch, and then made three distinct commits with each different version of the main `oais/index.md` text file. This makes comparing the versions easy (see below), but is a bit hacky and it would be better to make branches or tags work properly in the future. It might also make sense to split each chapter out into a separate file, to make the diffs more manageable.


Resources
---------

- The versions of the standard, via [CCSDS.org - Search CCSDS Publications](https://ccsds.org/searchpubs/?gv_search=650)
	- 2002 [CCSDS 650.0-B-1-S](https://ccsds.org/searchpubs/entry/3868/)
	- 2012 [CCSDS 650.0-M-2-S](https://ccsds.org/searchpubs/entry/3032/)
	- 2024 [CCSDS 650.0-M-3](https://ccsds.org/searchpubs/entry/3054/)
- [Standards process | OAIS Reference Model (ISO 14721)](http://www.oais.info/standards-process/) which includes a summary of changes
- [OAIS version 3 - what does it mean for repositories? | FAIR-IMPACT](https://fair-impact.eu/articles-and-blogs/oais-version-3-what-does-it-mean-repositories)
- [What you need to know about the recent updates in OAIS v3 | Preservica](https://preservica.com/resources/blogs-and-news/what-you-need-to-know-about-the-most-recent-oais-revision)


Technical Details
-----------------

Installing, with an attempt at including GPU-acceleration support ([as here](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local)).

```
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu130
pip install docling[easyocr] --extra-index-url https://download.pytorch.org/whl/cu130
```

Then ran, e.g.

```
docling --image-export-mode referenced pdfs/650x0m2s.pdf 
```

Not clear if GPC/CUDA support actually worked! Installing `easyocr` seemed to speed things up from 5 mins/PDF to 2 mins/PDF, with the results otherwise being 100% identical. Failing to use `rapidocr` was perhaps slowing it down?!

