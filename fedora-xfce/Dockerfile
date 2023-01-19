# https://github.com/danchitnis/container-xrdp

FROM fedora:latest

RUN dnf -y update

RUN dnf -y groupinstall xfce

RUN bash -c 'echo PREFERRED=/usr/bin/xfce4-session > /etc/sysconfig/desktop'

RUN dnf install -y xrdp xorgxrdp && dnf -y install sudo nload passwd nano gedit firefox chromium

# INSTALL VSCODE
RUN sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo && dnf check-update && dnf -y install code'


# Remove certain things due to errors
RUN dnf -y remove xfce4-power-manager && rm -rf /etc/xdg/autostart/xfce-polkit.desktop && dnf clean all


RUN dnf clean all

##### END of installations

COPY ./build/xrdp.ini /etc/xrdp/

COPY ./build/centos8-sesman.ini /etc/xrdp/
RUN mv /etc/xrdp/centos8-sesman.ini /etc/xrdp/sesman.ini

COPY ./build/startwm-xfce.sh /etc/xrdp/
RUN mv /etc/xrdp/startwm-xfce.sh /etc/xrdp/startwm.sh

RUN chmod a+x /etc/xrdp/startwm.sh

COPY ./build/run.sh /
RUN chmod +x /run.sh

EXPOSE 3389

ENTRYPOINT ["/run.sh"]

