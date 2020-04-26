FROM sagemathinc/cocalc-kubernetes-project

USER root

# Add current R version. Not all packages are available for 3.4
RUN apt update && \
    apt install apt-transport-https software-properties-common -y &&\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 &&\
    add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'

# Requirement for building some of the packages
RUN apt update && apt install libboost-all-dev libxml2-dev r-base r-base-dev pandoc-citeproc -y

# Reinstall R packages that were installed for older R version
RUN umask 022 \
  && echo "update.packages(checkBuilt=TRUE, ask=FALSE);" | R --no-save
  
# Install required R packages
RUN umask 022 \
  && echo "install.packages(c('rmarkdown', 'knitr', 'readr', 'tidyr', 'stringr', 'data.table', 'ggplot2', 'readxl', 'kableExtra', 'VGAM', 'OneR', 'multgee', 'gee', 'ordinal', 'effects', 'ggstatsplot', 'paramtest', 'shiny', 'plotly', 'bookdown'));" | R --no-save

# Install phantomjs for certain output of plotly 
RUN umask 022 \
  && echo "webshot::install_phantomjs()" | R --no-save
USER user

ENTRYPOINT ["/cocalc/bin/tini", "--"]
CMD ["sh", "-c", "env -i /cocalc/init/init.sh $COCALC_PROJECT_ID"]
