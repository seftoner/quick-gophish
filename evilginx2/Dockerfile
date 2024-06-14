# Use an official Debian image as the base
FROM debian:bullseye-slim

# Environment variables
ENV EVILGINX_HOME=/usr/local/evilginx2
ENV GO_VERSION=1.22.2

# Install dependencies
RUN apt-get update --quiet --quiet \
    && apt-get install --quiet --quiet --yes \
    git \
    gcc \
    make \
    bash \
    libc-dev \
    libpcap-dev \
    wget \
    ca-certificates

# Install Go
RUN wget https://golang.org/dl/go${GO_VERSION}.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz \
    && rm go${GO_VERSION}.linux-amd64.tar.gz

# Set Go environment variables
ENV PATH="/usr/local/go/bin:${PATH}"

# Install Node.js
# RUN curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh \
#     && bash nodesource_setup.sh \
#     $$ apt-get install -y nodejs

# Clone the evilginx2 repository
RUN git clone https://github.com/kgretzky/evilginx2.git ${EVILGINX_HOME}

# Set working directory
WORKDIR ${EVILGINX_HOME}

# Build the application
RUN make

# Expose necessary ports
EXPOSE 80 443

# Entry point to run evilginx2
ENTRYPOINT ["./bin/evilginx2"]
