---
title: guide - render markdown file to pdf for printing
categories:
  - by lazycoder
  - guide
description: it's just a little something i did and i would like to share how i did it
summary: how to render your markdown file into pdf for printing... also you can use multiple columns to make it look like a newspaper
tags: 
keywords: 
draft: false
weight: 0
aliases: 
showToc: false
cover:
  image: 
  alt: ""
  caption: ""
  relative: false
date: 2023-11-25T11:47
lastmod: 2024-03-11T00:00:00
publishdate: 2024-03-11T00:00:00
---
i wanted to render some markdown files into a pdf so that i can print them. it turned out harder than i expected.

the thing is, i searched far and wide but couldn't find a way to render markdown into multiple column pdf, but luckily i found pandoc and a lua filter which i used to render the markdown into multiple columns.

in order to use a font family i wanted, i installed tex live utility, which is used to install and manage my tex packages... which i used to install "fontaxes.sty" and "soul.sty", which apparently i need :|

i created a file called preconfig.tex with the following content for some layout configurations
```preconfig.tex
\renewcommand{\familydefault}{\sfdefault}
\usepackage{multicol}
\parindent 0px
```

and then i downloaded the lua filter at  <https://github.com/dialoa/columns/blob/master/columns.lua>


i had to join the markdown files all together, and also remove all the characters that latex cannot render.

```python
import re
def remove_emojis(data):
    emoj = re.compile("["
        u"\U0001F600-\U0001F64F"  # emoticons
        u"\U0001F300-\U0001F5FF"  # symbols & pictographs
        u"\U0001F600-\U0001F64F"  # emoticons
        u"\U0001F300-\U0001F5FF"  # symbols & pictographs
        u"\U0001F680-\U0001F6FF"  # transport & map symbols
        u"\U0001F1E0-\U0001F1FF"  # flags (iOS)
        u"\U00002702-\U000027B0"
        u"\U000024C2-\U0001F251"
        "]+", flags=re.UNICODE)

    data = re.sub(emoj, '', data)

    return data

import glob
things = glob.glob("./myfolder/*")


out = ":::{ .threecolumns columngap=1em }\n\n"


for thing in things:
    print(thing)
    if "thebookiwant" in thing:
        with open(thing,'r') as file:
            out += file.read()

out += ":::"

out = remove_emojis(out)


with open(f'processed.txt','w') as file:
    file.write(out)
```

this outputs a markdown file that joined all the selected markdown files together and put `:::{ .threecolumns columngap=1em }` at the start and `:::` at the end, so that the lua filter can process it.

finally, i made a little shell command executable to use pandoc to use the preconfig.tex and lua filter on the markdwon file to render the pdf

```
#!/usr/bin/env sh
pandoc "$1" -f markdown -t pdf -o "$1.pdf" -V geometry:margin=23pt -V fontsize=8pt --lua-filter=/path/to/md-columns.lua --include-in-header=/path/to/preconfig.tex
```

and that is how you render a markdown file into multi column pdf!
