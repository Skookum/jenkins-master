FROM jenkins/jenkins:lts-alpine

USER root

### Set up user for build execution and application runtime
# https://docs.openshift.com/container-platform/3.9/creating_images/guidelines.html#openshift-specific-guidelines
ENV APP_ROOT=/opt/app-root
VOLUME ${APP_ROOT}/logs ${APP_ROOT}/data
ENV PATH=${APP_ROOT}/bin:${PATH} HOME=${APP_ROOT}
COPY bin/ ${APP_ROOT}/bin/

### Pre-install default plugins
COPY plugins.txt ${APP_ROOT}/data/plugins.txt
RUN /usr/local/bin/install-plugins.sh < ${APP_ROOT}/data/plugins.txt

RUN chmod -R u+x ${APP_ROOT}/bin && \
    chgrp -R 0 ${APP_ROOT} && \
    chmod -R g=u ${APP_ROOT} /etc/passwd && \
    chgrp -R 0 "$JENKINS_HOME" && \
    chmod -R g=u "$JENKINS_HOME" && \
    chgrp -R 0 /usr/share/jenkins && \
    chmod -R g=u /usr/share/jenkins

USER jenkins

### Support user name recognition at runtime w/ an arbitrary UID - for OpenShift deployments
ENTRYPOINT ["/sbin/tini", "--", "uid_entrypoint"]
