FROM python:3.11-slim

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       git \
       build-essential \
       curl \
       ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user 'vscode' (same as official images)
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME

WORKDIR /workspace

# Ensure pip, wheel
RUN python -m pip install --upgrade pip setuptools wheel

# Install required Python packages in one command (simpler)
RUN pip install --user --no-cache-dir \
    "mkdocs>=1.5.0" \
    "mkdocs-material>=9.5.0" \
    "mkdocs-drawio-exporter>=0.8.0" \
    "mkdocs-glightbox>=0.3.0" \
    "pymdown-extensions>=10.0"

# Copy the rest of the repository into the image
COPY .. /workspace

USER $USERNAME

ENV PATH="/home/${USERNAME}/.local/bin:${PATH}"

CMD ["bash"]
