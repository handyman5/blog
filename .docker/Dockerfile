FROM python:3.11

# Add filter processing tools
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
    jpegoptim \
    optipng \
    tidy \
    emacs-nox \
    && rm -rf /var/lib/apt/lists/*

RUN pip install "Nikola[extras]"

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
