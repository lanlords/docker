# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
LABEL maintainer="Lanlords"

# Set environment variables
ENV USER bf1942
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
COPY --chown=bf1942:bf1942 data $HOME

# Copy configuration and scripts
COPY --chown=bf1942:bf1942 config/serversettings.con $HOME/mods/bf1942/settings/serversettings.con
COPY --chown=bf1942:bf1942 scripts/bf1942_wrapper $HOME/bf1942_wrapper

##################### INSTALLATION END #####################

# switch to user
USER $USER

# Expose the default ports
EXPOSE 14567/udp 22000/udp

# Set default container command
WORKDIR $HOME

ENTRYPOINT ["/data/bf1942_wrapper"]
CMD ["+dedicated", "+statusMonitor", "1"]
