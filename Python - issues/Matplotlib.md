**issuee**
  
      window = Tk.Tk(className="matplotlib")
       File "/usr/lib/python2.7/lib-tk/Tkinter.py", line 1822, in __init__
     self.tk = _tkinter.create(screenName, baseName, className, interactive, wantobjects, useTk, sync, use)
     _tkinter.TclError: couldn't connect to display ":0"


**Possible Solution:**

Matplotlib chooses Xwindows backend by default. You need to set matplotlib to not use the Xwindows backend.

Add this code to the start of your script (before importing pyplot) and try again:

        import matplotlib
        matplotlib.use('Agg')

Or add to `.config/matplotlib/matplotlibrc` line backend : Agg.

Or when connect to server use `ssh -X` ... command to use Xwindows.

Also you may try to export display: `export DISPLAY=mymachine.com:0.0`

And look through this page: [Generating a PNG with matplotlib when DISPLAY is undefined](https://stackoverflow.com/questions/2801882/generating-a-png-with-matplotlib-when-display-is-undefined)

https://github.com/matplotlib/matplotlib/issues/3466/

Install `tkinter` `tk-devl` https://stacks1.wordpress.com/2017/01/31/issue-with-tkinter-python-and-seaborn-_tkinter-tclerror-no-display-name-and-no-display-environment-variable/