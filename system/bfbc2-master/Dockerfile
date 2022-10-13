# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER bfbc2
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
 && apt-get install -y --no-install-recommends lib32stdc++6 lib32z1 lib32ncurses5 \
 && rm -rf /var/lib/apt/lists/*

# Create the application user
RUN useradd -m -d $HOME $USER

# Unpack the application files
COPY --chown=bfbc2:bfbc2 data $HOME

# Copy configuration
COPY --chown=bfbc2:bfbc2 config/config.ini $HOME/config.ini

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 9946/tcp 19021/tcp 19026/udp 19026/tcp 18390/tcp 18395/udp 18395/tcp

# Set default container command
WORKDIR $HOME
CMD $HOME/mase_bc2
