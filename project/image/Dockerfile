FROM sagemathinc/cocalc-kubernetes-project

USER root

# Requirement for building some of the packages
RUN apt update && apt install libboost-all-dev libxml2-dev r-base -y

# Install required R packages
RUN umask 022 \
  && echo "install.packages(c('rmarkdown', 'knitr', 'readr', 'tidyr', 'stringr', 'data.table', 'ggplot2', 'readxl', 'kableExtra', 'VGAM', 'OneR', 'multgee', 'gee', 'ordinal', 'effects'));" | R --no-save

USER user

ENTRYPOINT ["/cocalc/bin/tini", "--"]
CMD ["sh", "-c", "env -i /cocalc/init/init.sh $COCALC_PROJECT_ID"]
