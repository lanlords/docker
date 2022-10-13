# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER csgo
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 \
 && apt-get update -y \
 && apt-get install -y --no-install-recommends libstdc++6:i386 ca-certificates tar \
 && rm -rf /var/lib/apt/lists/*

# Create the application user
RUN useradd -m -d $HOME $USER

# Create the default directories
RUN mkdir -p $HOME/steam $HOME/$USER

# Change to steam directory
WORKDIR $HOME/steam

# Unpack the application files
ADD http://media.steampowered.com/installer/steamcmd_linux.tar.gz $HOME/steam/steamcmd_linux.tar.gz
RUN tar zxf steamcmd_linux.tar.gz \
 && rm $HOME/steam/steamcmd_linux.tar.gz
RUN $HOME/steam/steamcmd.sh +login anonymous +force_install_dir $HOME/$USER +app_update 740 validate +quit \
 && mkdir $HOME/.steam/sdk32 \
 && cp $HOME/steam/linux32/steamclient.so $HOME/.steam/sdk32/steamclient.so \
 && chown -R $USER:$USER $HOME

# Copy configuration
COPY --chown=csgo:csgo config/csgoserver.cfg $HOME/$USER/csgo/cfg/csgoserver.cfg
COPY --chown=csgo:csgo config/gamemode_competitive.cfg $HOME/$USER/csgo/cfg/gamemode_competitive.cfg

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 27015/udp 27015/tcp

# Set default container command
WORKDIR $HOME/$USER
CMD $HOME/$USER/srcds_run -game csgo -console -usercon -nobots -maxplayers_override 30 +mp_autoteambalance 0 -tickrate 128 +game_type 0 +game_mode 1 +mapgroup mg_bomb +ip 0.0.0.0 +exec csgoserver.cfg
