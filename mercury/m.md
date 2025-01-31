
# Create a Web App from Your Jupyter Notebook with Mercury

You can published you Notebook as an interactive web app with or without the code

![Image of a Jupyter Notebook by author](https://github.com/alanjones2/Alan-Jones-article-code/raw/master/mercury/images/Screenshot%202022-04-30%20170310.png)*Image of a Jupyter Notebook by author*

We all use Jupyter Notebooks to analyse and create visualizations of data , don't we? It's a great tool.

And of course you can share them by simply sending a copy to your colleagues. But an interactive app might be a better vehicle for those who don't care about your code but are interested in your results.

That is what Mercury from *mljar* promises. By simply adding a new cell at the beginning of your notebook you can get Mercury to convert the code into a web app that can be deployed to AWS, Heroku or wherever.

It also allows you to include interactive elements such as sliders, drop-downs to your notebook.

Below is a screen shot of a simple web app that I created in a few minutes. As you can see it includes a slider for interaction. The app is very simple: it loads a set of weather data and draws a charts of the monthly maximum temperatures for a particular year ' the slider allows you to select the year.

![Screenshot by author](https://cdn-images-1.medium.com/max/2000/1*uRYZ0QDl3xbyJhMoMAr_tg.png)*Screenshot by author*

More complex applications can be found on the [Mercury web site](https://mljar.com/mercury/). Here are a few:

![Image from the Mercury Github repo ' used with permission from mljar, AGPLv3 license](https://cdn-images-1.medium.com/max/2000/0*Yvuyfq6oPxAQ4dnN.png)*Image from the Mercury Github repo ' used with permission from mljar, AGPLv3 license*

But I'm going to walk through how to create the simple web app that I created. Mostly it's a very straightforward Jupyter notebook consisting of half a dozen cells.

### The notebook

The first is a *raw *cell that contains some YAML code that tells Mercury what to do and what interactions to include. The first three lines define the title, a description and set show-code to False. Setting this false means that the code in the cells will not be visible in the final web app.

    ---
    title: Exploring London Weather Data
    description: How to use mercury to create a web app
    show-code: False
    params:
       year:
          input: slider
          label: Select year
          value: 1952
          min: 1952
          max: 2018
    ---

The last lines define the parameters. year is a variable that will appear in the notebook and the lines that follow define a slider that will set the value of year. They are quite self-explanatory, I think. Note that the cell begins and ends with the line ---.

The second cell defines the variable year and gives it a value. Any variables that are referred to in the first cell must be defined together in a single cell like this.

    year = 1962

The next cell is a markup heading.

    **# Exploring London Weather Data**

We then import a couple of libraries.

    import numpy as np
    import pandas as pd

And some data.

    weather=pd.read_csv('heathrowDataFiltered.csv')

We then plot a graph filtering the data depending on the value of year. We print a message introducing the chart, too.

    weather[weather['Year']==year].plot(y='Tmax', x='Month',    
       legend=False)

    print(f"Monthly maximum temperatures for {year}")

![Image by author](https://github.com/alanjones2/Alan-Jones-article-code/raw/master/mercury/images/Screenshot%202022-04-30%20170856.png)*Image by author*

Running the notebook will result in the graph of monthly maximum temperatures for the year 1962, the value that we set at the beginning.

But the web app that we will create will allow us to select the year that we are interested in.

So, how do we do that?

### Mercury

First you need to install mercury:

    pip install mljar-mercury

Then you need to ÔÇÿadd' your notebook : on a command line type:

    mercury add <path_to_notebook>

And finally, you run it:

    mercury runserver --runworker

This will start up a server and you app will be running at the IP address 127.0.0.1:8000. Open this in a web browser and you see something like this:

![Image by author](https://cdn-images-1.medium.com/max/2422/1*rORiLw0rEVZHspSr7EGq0Q.png)*Image by author*

If you have added more than one notebook then they will all show up here. Click the open button for the app that you would like to run and you will see your notebook-based app.

![Screenshot by author](https://cdn-images-1.medium.com/max/2000/1*uRYZ0QDl3xbyJhMoMAr_tg.png)*Screenshot by author*

When the app is run it will display the chart; you can then adjust the slider and run it again to see the chart for the year that you have selected.

That was a very quick run through Mercury and only shows you some of its capabilities. There is much more on the Mercury website and especially in their [Github repo](https://github.com/mljar/mercury). For example, there is a whole bunch of input controls you can include, not just sliders, and the Github README document details all of the YAML commands that you can use and how to deploy your apps to the cloud. That's far more than I can cover here, so you really need to go and take a look.

You can download my files here: [data and notebook](https://github.com/alanjones2/Alan-Jones-article-code/tree/master/mercury)

As ever thanks for reading. If you would like to know when I publish articles you can get my occasional free newsletter, [Technofile](https://technofile.substack.com/) which is on Substack .
