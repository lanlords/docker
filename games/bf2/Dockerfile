# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER bf2
ENV HOME /data

################## BEGIN INSTALLATION ######################

# Create the application user
RUN useradd -m -d $HOME $USER

# Unpack the application files
COPY --chown=bf2:bf2 data $HOME

# Copy configuration
COPY admin/default.cfg $HOME/admin/default.cfg
COPY config/serversettings.con $HOME/mods/bf2/settings/serversettings.con

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 4711/tcp 16567/udp 29900/udp

# Set default container command
WORKDIR $HOME
CMD $HOME/start.sh +dedicated
