FROM registry.access.redhat.com/ubi8/python-36
LABEL name="Seldon Alibi Wrapper" \
      vendor="Seldon Technologies" \
      version="1.2.3-dev" \
      release="1" \
      summary="Alibi Explainer Wrapper for Seldon Core" \
      description="Allows Seldon Core inference models to run with a black box model explanation model from the Alibi:Explain project"

USER root
RUN pip install --upgrade pip
COPY setup.py setup.py
COPY alibiexplainer alibiexplainer
COPY README.md README.md

RUN pip install .

RUN chmod -R a+rwx /opt/app-root/lib/python3.6

# Add licences
RUN pip install pip-licenses
RUN mkdir ./licenses && pip-licenses --from=mixed --format=csv --output-file=./licenses/license_info.csv && \
    pip-licenses --from=mixed --format=plain-vertical --with-license-file --no-license-path --output-file=./licenses/license.txt
RUN mv ./licenses /licenses
USER default

ENTRYPOINT ["python", "-m", "alibiexplainer"]
