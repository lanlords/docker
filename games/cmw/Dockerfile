# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER cmw
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
RUN $HOME/steam/steamcmd.sh +login anonymous +force_install_dir $HOME/$USER +app_update 220070 validate +quit \
 && cp $HOME/steam/linux32/steamclient.so $HOME/$USER/Binaries/Linux/lib/steamclient.so \
 && echo 219640 > $HOME/$USER/Binaries/Linux/steam_appid.txt \
 && chown -R $USER:$USER $HOME

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 7777/udp 7778/udp

# Set default container command
WORKDIR $HOME/$USER/Binaries/Linux
CMD $HOME/$USER/Binaries/Linux/UDKGameServer-Linux AOCTO-Hillside_P\?steamsockets -seekfreeloadingserver -port=7777 -queryPort=7778
