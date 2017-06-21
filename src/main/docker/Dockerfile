# base image
FROM @dockerContainerFrom@

# install packages
RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories \
    && apk --update --no-cache add openrc motion

# configure openrc
RUN sed -i 's/#rc_sys=""/rc_sys="lxc"/g' /etc/rc.conf \
    && echo 'rc_provide="loopback net"' >> /etc/rc.conf \
    && sed -i 's/^#\(rc_logger="YES"\)$/\1/' /etc/rc.conf \
    && sed -i '/tty/d' /etc/inittab \
    && sed -i 's/hostname $opts/# hostname $opts/g' /etc/init.d/hostname \
    && sed -i 's/mount -t tmpfs/# mount -t tmpfs/g' /lib/rc/sh/init.sh \
    && sed -i 's/cgroup_add_service /# cgroup_add_service /g' /lib/rc/sh/openrc-run.sh

# configure motion
RUN sed -i 's/\(webcam_localhost\).*/webcam_localhost off/g' /etc/motion/motion-dist.conf \
    && sed -i 's/\(control_localhost\).*/control_localhost off/g' /etc/motion/motion-dist.conf \
    && sed -i 's/\(webcam_port\).*/webcam_port 8081/g' /etc/motion/motion-dist.conf \
    && sed -i 's/\(control_port\).*/control_port 8082/g' /etc/motion/motion-dist.conf

# define start services
RUN rc-update add motion default

EXPOSE 8081

CMD ["/sbin/init"]
