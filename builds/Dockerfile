ARG DESKTOP

FROM ghcr.io/linuxserver/rdesktop:ubuntu-$DESKTOP
# FROM ghcr.io/linuxserver/rdesktop:ubuntu-kde
# FROM ghcr.io/linuxserver/rdesktop:ubuntu-xfce
# FROM ghcr.io/linuxserver/rdesktop:ubuntu-mate

ARG BASE_URL

# Update (Firefox, CA, curl), install packages (Java 8 for ANYK, tzdata for timezone) and set timezone
RUN apt-get update && apt-get --only-upgrade install firefox ca-certificates curl && apt-get install -y \
    openjdk-8-jre tzdata \
    && ln -fs /usr/share/zoneinfo/Europe/Budapest /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && apt-get autoremove && apt-get clean -y && rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/* /var/log/*

RUN echo "Installing..." \
    # Create 'Desktop' folder for user 'root' so the ANYK installer can create a shortcut there
    && mkdir ~/Desktop \
    # Download and install ANYK
    && curl $BASE_URL -o ~/abevjava_install.jar \
    # -s: silent (non-gui) install
    # -u: create user settings
    && java -jar ~/abevjava_install.jar -s -u \
    && rm ~/abevjava_install.jar \
    # Change rights to default user 'abc'
    && chown -R abc:abc /usr/share/abevjava/ \
    && chown -R abc:abc /root/.abevjava/ \
    && chown abc:abc /etc/abevjavapath.cfg \
    # Create 'Desktop' folder for default user
    && mkdir /config/Desktop \
    # Copy the ANYK shortcut to the user Desktop
    && cp ~/Desktop/ÁNYK.desktop /config/Desktop/
