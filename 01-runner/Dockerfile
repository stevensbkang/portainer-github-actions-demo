FROM ubuntu:20.04
ARG RUNNER_VERSION="2.288.1"
ARG RUNNER_USERNAME="runner"

RUN apt-get update -y \
  && apt-get upgrade -y \
  && useradd -m $RUNNER_USERNAME
RUN apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    jq

RUN mkdir /home/$RUNNER_USERNAME/actions-runner && cd /home/$RUNNER_USERNAME/actions-runner \
  && curl -O -L https://github.com/actions/runner/releases/download/v${RUNNER_VERSION}/actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz \
  && tar xzf ./actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz

WORKDIR /home/$RUNNER_USERNAME/actions-runner
RUN chown -R runner /home/runner \
  && bin/installdependencies.sh \
  && chmod +x run.sh

USER ${RUNNER_USERNAME}
ENTRYPOINT ["run.sh"]