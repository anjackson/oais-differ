OAIS Differ
===========

Using Markdown and GitHub to see how the OAIS has changed.

- Downloaded each version of the OAIS standard PDF
- Used [Docling](https://docling-project.github.io/docling/) to convert PDF to Markdown.
- Used an editor to normalise spaces `:%s/ +/ /g`
- Committed the results to git branches and pushed to GitHub.


Result: <https://github.com/anjackson/oais-differ/compare/2012...2024?diff=split&w#diff-c0866066239b8a685db373713dbb89e8192ddcfcfbf6052e5579035c8e67b74f>

(it's the last entry, at the bottom, and you'll have to click to make it load the large diff)


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

