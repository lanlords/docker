# Set the base image to Ubuntu
FROM ubuntu:18.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER bt1944
ENV HOME /data

# Enable pipefail for shell commands
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN echo steam steam/question select "I AGREE" | debconf-set-selections \
 && echo steam steam/license note '' | debconf-set-selections
RUN dpkg --add-architecture i386 \
 && apt-get update -y \
 && apt-get install -y --no-install-recommends ca-certificates tar steamcmd \
 && rm -rf /var/lib/apt/lists/*

# Create the application user
RUN useradd -m -d $HOME $USER

# Create the default directories
RUN mkdir -p $HOME/steam $HOME/$USER $HOME/$USER/Userdir $HOME/$USER/Logs

# Change to steam directory
WORKDIR $HOME/steam

# Install the game via steamcmd
RUN /usr/games/steamcmd +login anonymous +force_install_dir $HOME/$USER +app_update 805140 validate +quit \
 && chown -R $USER:$USER $HOME

# Copy configuration
COPY --chown=bt1944:bt1944 config/DefaultGame.ini $HOME/$USER/DefaultGame.ini

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 7777/udp 7777/tcp 7780/udp 7780/tcp

# Set default container command
WORKDIR $HOME/$USER
CMD $HOME/$USER/Linux/Battalion/Binaries/Linux/BattalionServer /Game/Maps/Final_Maps/Derailed?Game=/Script/ShooterGame.BombGameMode?listen -broadcastip="0.0.0.0" -PORT=7777 -QueryPort=7780 -log -logfilesloc="/data/bt1944/Logs" -userdir="/data/bt1944/Userdir" -defgameini="/data/bt1944/DefaultGame.ini"
