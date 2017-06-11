FROM python:3.4

# Last update: 2016-06-08
RUN apt-get update -qq && apt-get install -y \
  libgdal1h gdal-bin libgdal-dev \
  libblas-dev liblapack-dev libatlas-base-dev \
  gfortran && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

RUN pip --no-cache-dir install \
    ipykernel numpy scipy scikit-learn jupyter matplotlib pandas tensorflow seaborn scikit-image && \
    python -m ipykernel.kernelspec

COPY ./config/jupyter_notebook_config.py /root/.jupyter/

# Jupyter has issues with being run directly:
# https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY ./config/run_jupyter.sh /

# Jupyter
EXPOSE 8888

VOLUME "/notebooks"
VOLUME "/input"
VOLUME "/output"
WORKDIR "/notebooks"

CMD ["/run_jupyter.sh"]
