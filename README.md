## Instructions for running analysis
This repo has all the materials to run the walkability analysis presented at Maptime Wellington (July '21). All packages required for the analysis are specified in `environment.yml`. To make it easy to run the code, there is a `Dockerfile` that creates a container with the Jupyterlab IDE and all the project dependencies installed within. To run the container, you need to: 
- Install [Docker](https://docs.docker.com/get-started/)
- Clone this repo
```
git clone https://github.com/shriv/maptime-jul21.git
```
- Go to the repository directory 
- Get the image locally building the container. To build the container on a unix / linux terminal the command is as below. Note, it can take a while ~10-15 minutes. 
```
docker build -t maptime-jul21 .
```
- Run the container 
```
docker run -d -p 8888:8888 -v ${PWD}:/home/jovyan/work \
-e JUPYTER_ENABLE_LAB=yes \ 
-e CHOWN_HOME=yes \
-e CHOWN_HOME_OPTS='-R' 
maptime-jul21 \ 
start.sh jupyter lab --LabApp.token=\'\'
```
- Go to the IDE served on localhost:8888
![](./assets/jupyterlab-launcher.png)
- The notebook is mounted to the `work` directory. You can run cells with `Shift+Enter`. Or, `Run/Run * Cells` commands in the dropdown. 
![](./assets/jupyterlab-notebook.png)

## Creating slides 
The presented slides can be seen [here](https://shriv.github.io/maptime-jul21/index.slides#/). Any changes to the notebook that need to be in the slides requires them built again. They are created from the executed Notebook using `nbconvert` pre-installed in the image. To set up the slide transitions, follow instructions [here](https://jupyterlab.readthedocs.io/en/stable/user/export.html#reveal-js-slides). Then, export the notebook as html slides from the terminal (reached from the Jupyterlab Launcher). You might need to do `cd work` before running the following to be in the working directory of the notebook. 

```
jupyter nbconvert  Walking\ to\ the\ park\ on\ a\ computer.ipynb \ 
--to slides \ 
--no-prompt \ 
--TagRemovePreprocessor.remove_input_tags='{"remove"}' \ 
--output "index"
```

You can now see these slides in a browser by opening the `index.slides.html` file created in the repository.  If you fork this repository, [you can set it up as a `Github Pages` repository](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site). The committed html slides file will now be served as a webpage on `https://<username>.github.io/<repository-name>/index.slides#/`. 

## Learning resources
- [Introduction to OpenStreetMap](https://learnosm.org/en/beginner/introduction/)
- [Introduction to Jupyterlab and Python for plotting](https://swcarpentry.github.io/python-novice-gapminder/aio/index.html)
- [Geospatial analyses with Python](https://geographicdata.science/book/index.html)
- [Examples of network analysis and exploring OSM data with `osmnx`](https://github.com/gboeing/osmnx-examples/tree/main/notebooks)
- [Geospatial network analysis coursework in lectures 07 and 08](https://github.com/gboeing/ppd599/tree/main/modules)
- [Pandana for many to many routing](https://github.com/UDST/pandana/blob/dev/examples/Pandana-demo.ipynb)

