# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER tf2
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 \
 && apt-get update -y \
 && apt-get install -y --no-install-recommends libcurl3-gnutls:i386 libstdc++6:i386 lib32gcc1 lib32ncurses5 ca-certificates tar \
 && rm -rf /var/lib/apt/lists/*

# Create the application user & create default directories
RUN useradd -m -d $HOME $USER \
 && mkdir -p $HOME/steam $HOME/$USER

# Change to steam directory
WORKDIR $HOME/steam

# Unpack the application files
ADD http://media.steampowered.com/installer/steamcmd_linux.tar.gz $HOME/steam/steamcmd_linux.tar.gz
RUN tar zxf steamcmd_linux.tar.gz \
 && rm $HOME/steam/steamcmd_linux.tar.gz
RUN $HOME/steam/steamcmd.sh +login anonymous +force_install_dir $HOME/$USER +app_update 232250 validate +quit \
 && mkdir $HOME/.steam/sdk32 \
 && cp $HOME/steam/linux32/steamclient.so $HOME/.steam/sdk32/steamclient.so \
 && chown -R $USER:$USER $HOME

# Copy configuration
COPY config/server.cfg $HOME/tf2/tf/cfg/server.cfg

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 27015/udp 27015/tcp

# Set default container command
WORKDIR $HOME/$USER
CMD $HOME/$USER/srcds_run -console -game tf -nohltv +maxplayers 32 -port 27015 +sv_lan 1 +exec server.cfg +ip 0.0.0.0 +map plr_pipeline
