# https://raps-with-r.dev/repro_cont.html


# Windows: your docker file name should be "Dockerfile"!!!

# stating that it’s based on the Ubuntu Jammy (so version 22.04) operating system
FROM ubuntu:jammy

# First we define a variable using ENV, called TZ and we set that to the Europe/Berlin time zone
# We had to do all this, because when we will later install R, a system-level dependency called tzdata gets installed alongside it. 
# This tool then asks the user to enter his or her time zone interactively. 
# By using these two commands, we can set the correct time zone and once tzdata gets installed, that tool doesn’t ask for the time zone anymore, so the build process can continue.
ENV TZ=Europe/Berlin

# uses Ubuntu’s package manager to first refresh the repositories (this ensures that our local Ubuntu installation repositories are in sync with the latest software updates that were pushed to the central Ubuntu repos)
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# we use Ubuntu’s package manager to install r-base
RUN apt-get update && apt-get install -y r-base

# command that will be executed when we run the container
CMD ["R"]



# sign in to hub.docker
# 
# docker tag raps_ubuntu_r ulrikeniemann/raps_ubuntu_r
# docker push ulrikeniemann/raps_ubuntu_r