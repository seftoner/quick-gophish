FROM ubuntu:latest

# Environment variables
ENV PROJECT_DIR="/app/src/evilginx2"
ENV EVILGINX_BIN="/app/bin/evilginx"

# Install dependencies
RUN apt-get update --quiet --quiet \
    && apt-get install --quiet --quiet --yes \
    git \
    gcc \
    make \
    golang

# Clone the evilginx2 repository
RUN git clone https://github.com/kgretzky/evilginx2.git ${PROJECT_DIR}

# Set working directory
WORKDIR ${PROJECT_DIR}

# Build the application
RUN make \
    && mkdir /app/bin \
    && cp ${PROJECT_DIR}/build/evilginx ${EVILGINX_BIN}

WORKDIR /app

# Expose necessary ports
EXPOSE 80 443

# COPY ./docker-entrypoint.sh /opt/
# RUN chmod +x /opt/docker-entrypoint.sh

CMD [${EVILGINX_BIN}, "-p", "/app/phishlets"]
