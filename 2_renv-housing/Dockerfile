# https://raps-with-r.dev/repro_cont.html


# Windows: your docker file name should be "Dockerfile"!!!

# rocker-project: https://rocker-project.org/ - R-ready docker images
# R-versioned
# The first line states that we will be basing our image on the image from the Rocker project that ships with R version 4.2.2, which is the right version that we need. 
# see needed R-Version in renv.lock
FROM rocker/r-ver:4.2.2

# Then, we install the required system-level dependencies using Ubuntu’s package manager
RUN apt-get update && apt-get install -y \
    libglpk-dev \
    libxml2-dev \
    libcairo2-dev \
    libgit2-dev \
    default-libmysqlclient-dev \
    libpq-dev \
    libsasl2-dev \
    libsqlite3-dev \
    libssh2-1-dev \
    libxtst6 \
    libcurl4-openssl-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    libxt-dev \
    unixodbc-dev \
    wget \
    pandoc

# Then comes the {remotes} package. This will allow us to download a specific version from {renv} from Github, which is what we do in the next line.
RUN R -e "install.packages('remotes')"

# see needed version of renv in renv.lock: 1.0.5
# Error in utils::download.file(url, path, method = method, quiet = quiet,  : 
# kann URL 'https://api.github.com/repos/rstudio/renv/tarball/1.0.5' nicht öffnen
# 0.16.0
RUN R -e "remotes::install_github('rstudio/renv@0.16.0')"

# creates a folder (mkdir stands for make directory), inside the Docker image
RUN mkdir /home/housing
 
# copies the renv.lock file from our computer (save this file next to the Dockerfile) to /home/housing/renv.lock
# By doing this, we include the renv.lock file inside of the Docker image which will be crucial for the next and final step
COPY renv.lock /home/housing/renv.lock

# runs the R program from the Linux command line
# Using R -e will quickly become a habit, because this is how you can run R non-interactively, from the command line.
# restore the packages from the renv.lock file that we copied before
RUN R -e "setwd('/home/housing/');renv::init();renv::restore()"


# Build the image using docker build -t housing_image . (don’t forget the . at the end).

# run container
# docker run housing_image

# log in into a command line inside a running docker container
# docker run --rm -it --name housing_container housing_image bash

# move to the folder
# cd home/housing

# start R interpreter
# R

# try to load package
# library("housing")

# success :)