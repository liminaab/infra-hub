FROM jenkins/jnlp-slave:alpine

USER root

RUN apk add --no-cache curl docker gettext musl-dev tzdata jq python3 gcc libffi-dev openssl-dev perl sshpass python3-dev zip \
 && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
 && python3 get-pip.py \
 && pip install --upgrade pip setuptools\
 && pip install pyyaml \
 && pip install openshift \
 && pip install ansible

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl

RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 && \
    chmod 700 get_helm.sh && ./get_helm.sh && rm get_helm.sh && helm plugin install https://github.com/chartmuseum/helm-push

RUN mkdir -p /root/bin && curl -o /root/bin/aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/linux/amd64/aws-iam-authenticator && \
    chmod +x /root/bin/aws-iam-authenticator 

ENV PATH "/root/bin:$PATH"



ENTRYPOINT ["jenkins-slave"]
