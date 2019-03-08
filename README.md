# WoltSummerProject

## Pick-up median time ##

<p>I recently got to see this years' Wolt project and decided to present here my Python Jupyter notebook version of solution for Wolt Summer Coding Task 2019.
In order to run the pick-up time I decided to go for widgets that make the code more interactive and reduce the risk of errors when selecting the desired timeframe analysis.
I hope you'll like it! :) </p>

## Steps for running and using the file ##

1. Use git clone or click download button to download this repo.
2. Go to the command line inside the folder with the stored repo: <b>cd downloaded-repo-folder-name</b>.
3. In the folder command line install the following packages set:
* <b>pip install python3</b>
* <b>pip install virtualenv</b> -> once done <b>run virtualenv venv</b>, then <b>source venv/bin/activate</b> (to enter in the virtual environment)
* from inside the virtual environment <b>run pip install pandas numpy ipywidgets jupyter</b>
* after the <b>ipywidgets</b> are installed <b>run jupyter nbextension enable --py widgetsnbextension</b>;it should return a message ending with <i>Validating: OK</i>
* lastly, <b>run jupyter notebook</b> in the folder command line
4. The browser will open and show all the contents of the cloned repo. Two files contain the raw data that was analyzed and the <i>.ipynb</i> document is the part that can be used to track the median time calculation.
5. Open the .ipynb file and check the <b>chapter 5</b>: inside are the widgets for choosing the date and hours of reference.

<p><b>Note</b>: after choosing the date( in chapter 5), to run the saved data you need to press <i>Shift+Enter</i> except for the 2nd widget where the hour is manually selected. That function will be skipped, otherwise the selected data would be resetted. 
At the end of the file will appear all the median pick-up times, as organized by date and hour.
Also, in case the <b>pickup_times.csv</b> file is changed with a differently named doc, in <b>chapter 1</b> of the <b>.ipynb</b> file the data source name has to be updated too.</p>
