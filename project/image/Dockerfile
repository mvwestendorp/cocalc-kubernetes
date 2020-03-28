FROM sagemathinc/cocalc-kubernetes-project

USER root

RUN apt update && apt install libboost-all-dev -y
RUN umask 022 \
  && echo "install.packages(c('readr', 'tidyr', 'stringr', 'data.table', 'ggplot2'));" | R --no-save

USER user

ENTRYPOINT ["/cocalc/bin/tini", "--"]
CMD ["sh", "-c", "env -i /cocalc/init/init.sh $COCALC_PROJECT_ID"]