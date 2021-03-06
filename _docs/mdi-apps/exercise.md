---
title: "EXERCISE"
parent: MDI Apps
has_children: false
nav_order: 10
---

## {{ page.title }}

In this exercise you will learn how to develop an MDI app.
As a high-level overview, you will:

- use a batch script to install the MDI on your personal computer
- launch the web server by running it on your computer
- add the demo tool suite to your MDI installation
- modify the demo app by adding an appStep to run your mtcars plotter

### Prerequisites

To complete the instructions below you should have completed 
these exercises:

- MDI Pipelines >> EXERCISE #1
- R and Shiny >> EXERCISE #3

### STEP #1 - Download an MDI batch script for your PC

MDI apps run equivalently on any computer that can run R -
this includes your PC, which is where you will do most development
work on Stage 1 Apps.  

There are several ways to install and run the MDI locally, but
we recommend downloading a batch script customized for your computer
using our **batch script generator**:

- <https://wilsonte-umich.shinyapps.io/mdi-script-generator/>

Click on the **Configure** tab, then select **Local Computer**. Click into
the rest of the options to see their documentation to
decide if you need specific values or can use the defaults.
You might want to change the Installation or R Source Directories.
Do not use Host or Data Directories.

Once configured, click the **Download** tab, select the appropriate
operating system and download the script.

### STEP #2 - Install the MDI web server on your PC

Follow the instructions on the script generator **Usage**
page to execute your batch script, accepting any security challenges
(or not, but then you can't proceed). After executing your script, you
should see a terminal window like:

```bash
Welcome to the Michigan Data Interface.

  MDI_DIRECTORY    'C:/mdi'
  HOST_DIRECTORY   NULL
  DATA_DIRECTORY   NULL
  R_DIRECTORY      C:/Program Files/R/R-4.1.2
  INSTALL_N_CPU    4
  DEVELOPER        FALSE

What would you like to do?

  1 - (re)install the MDI on your computer
  2 - run the MDI web interface locally
  3 - exit and do nothing

Select an action by its number:
```

Type "1" and hit Enter to **execute the installation**, typing "y" for "yes"
at the confirmation prompt.

It will takes several minutes to complete the installation
as many R packages need to be installed (the MDI
installation itself is quick).

### STEP #3 - Run the MDI web server on your PC

Once the installation is complete, you will see the same prompt
as shown above. Now type "2" and hit Enter to **launch the
MDI apps interface**. A web browser will open.

What is happening is that your computer is acting as both the
web server (in your terminal window) and the web client (in your browser).
Take a look at the output in the terminal window to see the progress
log being generated by the server as you interact with apps in the browser.

{% include figure.html file="R/mdi-local.png" %}

### STEP #4 - Add the mdi-demo-tools suite to your installation

At this point you are running the framework but no apps, so you
can't really do anything yet! Let fix that by **adding the MDI 
demo tool suite to your installation**:

- <https://github.com/MiDataInt/demo-mdi-tools>

You add a tool suite by **editing file _config/suites.yml_** 
under your MDI installation folder. There are two ways to do it - 
pick whichever your prefer:

- open  _config/suites.yml_ in your code editor
- click the gear, i.e., cog, icon at the top of your browser and select _suites.yml_

Edit the file to include the entry:

```yml
# config/suites.yml
suites:
  - MiDataInt/demo-mdi-tools
```

**Save** your edits.  

If you chose to edit _suites.yml_ in the app, it will install the tool suite
immediately.  If you were working in a code editor, you need to stop
your server and **re-run the installation from Step #2** above, which will go
much faster now, then re-launch the server.

Finally, **validate your installation of the demo suite** by loading your previous 
demo pipeline data package into the MDI launch page. It should launch
the demo app, just as it did on our public server in a previous exercise.

### STEP #5 - Add a new appStep to mdi-demo-tools

Finally, we will edit the demo app to add one more appStep tab called
"4 - Basic Training".

Your first job is to **find the app scripts**, which will be in folder
_/mdi/suites/definitive/demo-mdi-tools/shiny/apps/demo_. Open that folder
in your code editor.

To help you get started, the demo app includes the shell of the new app
step ready to take your mtcars code. 
Your first goal is to activate the app step by 
**uncommenting the basicTraining appStep in _config.yml_**:

```yml
# apps/demo/config.yml
appSteps:
    upload: # nearly always the 1st step of every app
        module: sourceFileUpload
        shortLabel: "Adjust Data Sources"
        shortDescription: "Drag and drop additional source data file(s)."
    display: # usually the 2nd step of every app
        module: displayResults
    withCode:
        module: withCode
    basicTraining: # !! REMOVE THE COMMENT MARKS FROM THIS SECTION !!
        module: basicTraining
```

Now **reload your web browser**
into the demo app to see the new tab (**hint**: click on the "MDI"
text at the upper left corner to reload the page). Click on your new tab
to see a few initial UI elements.

Finally, edit the following two files to 
**fill the Basic Training page with your mtcars code**:
- apps/demo/modules/appSteps/basicTraining/basicTraining_ui.R
- apps/demo/modules/appSteps/basicTraining/basicTraining_server.R

Here's what you need to understand: previously, your app had
a UI and a server function for the _entire app_. When embedding 
your code into an MDI app step, you still have a ui and server function,
but now they define an _appStep module_.
You can think of it as an "app within an app". 
Otherwise, the organizational concept is the same:
- declare inputs and outputs in _basicTraining_ui.R_
- react to inputs and fill outputs in _basicTraining_server.R_

You'll soon see how quickly you can elaborate complex apps when
all you have to do is declare and populate app steps.

### STEP #6 - Demonstrate your success

Email your mentor a screen shot of your web browser running
your mtcars code within the MDI demo app under the Basic Training step.
