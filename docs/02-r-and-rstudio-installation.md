# R and RStudio: Installation and Setup




In this chapter, we will walk you through the process of installing R and the desktop version of RStudio. Although you will need to install both R and RStudio, once they are installed you will only interact with RStudio when you compute. 

<div class="figure" style="text-align: center">
<img src="figs/01-rstudio-and-r.png" alt="Workflow for using R: Once both appplications are installed on you computer, you will only interact with R through RStudio." width="60%" />
<p class="caption">Workflow for using R: Once both appplications are installed on you computer, you will only interact with R through RStudio.</p>
</div>

<br /><br />


## Installing R

To install R, navigate your web browser to:

<p style="margin-left:auto; margin-right:auto;">https://www.r-project.org/</p>

Then,

- Click the `CRAN` link under `Download` on the left-hand side of the page.
- Select a mirror site. These should all be the same, but I tend to choose the `Iowa State University` link under `USA`.^[When internet used to be dial-up (i.e., super slow, you wanted to choose a mirror site  that was closest in proximity to your location as it sped up the download. This is less of a concern now that internet download speeds are much faster.]
- In the `Download and Install R` box, choose the binary that matches the operating system (OS) for your computer.

This is where the installation directions diverge depending on your OS.

**Mac Instructions**

So long as you are running MacOS 10.13 or higher just click the first link for the PKG, which will download the installer for the most current version of R (4.0.2 as of July 24, 2020). Once the download completes, open the installer and follow the directions to install R on your computer.

If you are running an older version of MacOS, click the `el-capitan/base` link (near the bottom of the page) and then select the PKG link for R 3.6.3. Once the download completes, open the installer and follow the directions to install R on your computer.

If you are unsure which version of the MacOS is running on your computer, select `About this Mac` from the Apple menu in your toolbar. 


**Windows Instructions**

Click the link that says `Install R for the first time` (or click `base`; they go to the same place). Then click the `Download R 4.0.2 for Windows` link, which will download the installer for the most current version of R (4.0.2 as of July 24, 2020). Once the download completes, open the installer and follow the directions to install R on your computer.

**Linux Instructions**

If you are running Linux, you should know how to install things on your computer. 🙋


<br /><br />


## Installing RStudio Desktop


After you have installed R, you next need to install RStudio Desktop. To do this, navigate your web browser to:

<p style="margin-left:auto; margin-right:auto;">https://rstudio.com/products/rstudio/download/</p>

Then,

- Select the blue `Download` button under the free, open-source version of RStudio Desktop.
- Select the installer associated with your computer's OS.
- Once the download completes, open the installer and follow the directions to install RStudio Desktop on your computer.

<br /><br />


## Checking that Things Worked

From your Applications or Programs folder, open RStudio. If you have successfully downloaded both programs, this should open the application and you should see a message indicating that you are using "R version 4.0.2" in the console pane.

<div class="figure" style="text-align: center">
<img src="figs/02-opening-rstudio.png" alt="Once you open RStudio, you should see a message indicating that you are using `R version 4.0.2` in the console pane. Here the console pane is on the left-side, but it may be in a different location for you. Your RStudio may also have a white background rather than the black background seen here." width="100%" />
<p class="caption">Once you open RStudio, you should see a message indicating that you are using `R version 4.0.2` in the console pane. Here the console pane is on the left-side, but it may be in a different location for you. Your RStudio may also have a white background rather than the black background seen here.</p>
</div>

<br /><br />


## Customizing RStudio

While the information in this section is not crucial for making things work, it is useful to get RStudio looking good and setting some default settings. Open the `Tools > Options` menu (Windows) or `RStudio > Preferences` (Mac). 

<div class="figure" style="text-align: center">
<img src="figs/06-options.png" alt="The RStudio options/preferences menu has many settings to customize RStudio." width="50%" />
<p class="caption">The RStudio options/preferences menu has many settings to customize RStudio.</p>
</div>


- In the `General` settings (`Basic`), change the option on "Save workspace to .Rdata on exit" to be "Never". Click the "Apply" button.
- In the `Appearance` settings, customize the look of RStudio to something aesthetically appealing to you. When you are finished, click the "Apply" button.
- There are also options you can set in the `Accessibility` settings if you use a screen reader. If you change anything, don't forget to click the "Apply" button.

When you are finished customizing RStudio, click the "OK" button.


<br /><br />



## Install Rtools/Command Line Tools

You may need to install some additional functionality to your system in order to get certain packages to install or load properly. On a Windows machine, you might need to install *Rtools*. Mac users might need to add the *Command Line Tools*. These tools also allow you to write and compile your own R packages. RStudio has well written instructions for adding these tools at: https://support.rstudio.com/hc/en-us/articles/200486498-Package-Development-Prerequisites.


<br /><br />


