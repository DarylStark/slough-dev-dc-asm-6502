# hadolint ignore=DL3007
FROM dast1986/slough-dev-dc-generic-base:1.0.0 AS base

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Switch to root user
USER root

# Intall 6502 ASM tools
# hadolint ignore=DL3008
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    cc65 \
    hexedit && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists

# Copy the needed files
COPY --chown=developer:developer linker_config_example.cfg /home/developer/
COPY --chown=developer:developer README.md /home/developer/

# Switch back to developer user
USER developer

# Add PATH
# hadolint ignore=SC2016
RUN echo 'export PATH=$PATH:~/.local/bin' >> /home/developer/.bashrc.local

# Install py65mon
RUN /home/developer/.cargo/bin/uv self update && \
    /home/developer/.cargo/bin/uv tool install py65

# Configure Starship
ENV PROMPTNAME="ASM6502"

# Set the default command to bash
CMD ["bash"]