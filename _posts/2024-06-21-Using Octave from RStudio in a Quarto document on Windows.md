---
layout: post
title:  "Using Octave from RStudio in a Quarto document on Windows"
date:   2024-06-21 09:00:00 +0100
tags: Octave, RStudio, Quarto, Windows, Open Science
---

_Just putting this out there in the vague hope that someone (possibly future me) finds it instead of wasting a whole bunch of time trying to work this out._

To use a different engine for running code in a Quarto document you need to manually set the path to that engine.
Lots of places quote the path for Octave as `'/usr/local/opt/octave/bin/octave'` or some version of that, but I think that much be what it is on Linux.
And sure, it makes sense that if you're using Octave (open source), RStudio (open source), and Quarto (open source), you might be on an open source operating system, but I'm not.
So, the path _I_ needed was: `C:/Program Files/GNU Octave/Octave-6.1.0/mingw64/bin/octave-cli.exe`

Full MWE:
````

---
title: "test"
format: html
editor: visual
---

## Quarto

Quarto enables you to weave together content and executable code into a finished document. To learn more about Quarto see <https://quarto.org>.

## Running Code

When you click the **Render** button a document will be generated that includes both content and the output of embedded code. You can embed code like this:


```{r}
1 + 1
```

```{octave,engine.path="C:/Program Files/GNU Octave/Octave-6.1.0/mingw64/bin/octave-cli.exe",results='asis',echo=TRUE}
  x = -10:0.1:10;
  plot (x, sin (x)); 
  print -djpg myfigure.jpg 
```

More text and then import the generated figure from Octave. ![My Plot of the sin-function with Octave](./myfigure.jpg)

````

A couple of oddities:
- I tried updating my version of Octave (to 9.2.0) but then when I tried to Render, it just hung forever.
- If I don't include that little r codechunk before, I get an error:
```
Starting python3 kernel...Traceback (most recent call last):
  File "C:\PROGRA~1\RStudio\resources\app\bin\quarto\share\jupyter\jupyter.py", line 21, in <module>
    from notebook import notebook_execute, RestartKernel
  File "C:\PROGRA~1\RStudio\resources\app\bin\quarto\share\jupyter\notebook.py", line 14, in <module>
    from yaml import safe_load
ModuleNotFoundError: No module named 'yaml'
Python 3 installation:
  Version: 3.10.4
  Path: C:/Users/cege-user/AppData/Local/Programs/Python/Python310/python.exe
  Jupyter: (None)

Jupyter is not available in this Python installation.
Install with py -m pip install jupyter
```

Now to try and get it to deploy remotely with a [GitHub action](https://quarto.org/docs/publishing/github-pages.html#executing-code), ~~and the world shall be mine...~~ we'll have a viable way to reproducibly generate a nice looking document with some Octave code running within it...  
