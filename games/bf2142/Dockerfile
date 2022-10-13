# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER bf2142
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Update the repository and install prerequisites
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 \
 && apt-get update -y \
 && apt-get install -y --no-install-recommends libc6-i386 lib32ncurses5 libc6-dev-i386 \
 && rm -rf /var/lib/apt/lists/*

# Create the application user
RUN useradd -m -d $HOME $USER

# Unpack the application files
COPY --chown=bf2142:bf2142 data $HOME

# Copy configuration
COPY admin/default.cfg $HOME/admin/default.cfg
COPY config/serversettings.con $HOME/mods/bf2142/settings/serversettings.con

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 14567/udp

# Set default container command
WORKDIR $HOME
CMD $HOME/bf2142_lnxded +dedicated +statusMonitor 1
