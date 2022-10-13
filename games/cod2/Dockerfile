# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER cod2
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 \
 && apt-get update -y \
 && apt-get install -y --no-install-recommends libstdc++5:i386 \
 && rm -rf /var/lib/apt/lists/*

# Create the application user
RUN useradd -m -d $HOME $USER

# Unpack the application files
COPY --chown=cod2:cod2 data $HOME

# Copy configuration
COPY --chown=cod2:cod2 config/server.cfg $HOME/main/server.cfg

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 28960/udp 20510/udp

# Set default container command
WORKDIR $HOME
CMD $HOME/cod2_lnxded +set dedicated 1 +set g_gametype ctf +map_rotate +set sv_punkbuster 0 +exec server.cfg
