FROM --platform=$BUILDPLATFORM rockylinux:9.3

ARG BRANCH_NAME

# Install Base OS Dependencies
RUN dnf update -y && \
    dnf install -y epel-release && dnf clean all && \
    dnf install -y \
	python3.12 \
	libjson-glib-dev \
	git && \
    dnf clean all

RUN alternatives --install /usr/bin/python3 python /usr/bin/python3.12 1

RUN python3 --version

# Canary install
RUN python3 -m venv canary && \
    . canary/bin/activate && \
    python3 -m pip install --upgrade pip==25.1.1 && \
    python3 -m pip install -e git+https://git@github.com/alexknigge/canary@$BRANCH_NAME#egg=canary-wm[dev]
    python3 -m pip install flux-python


COPY test.sh .
ENTRYPOINT ["/bin/bash", "-c"]
