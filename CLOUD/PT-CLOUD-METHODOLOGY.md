From hacktricks online site + my modifications + comments 

Basic Methodology

Each cloud has its own peculiarities but in general there are a few common things a pentester should check when testing a cloud environment:

    Benchmark checks

        This will help you understand the size of the environment and services used

        It will allow you also to find some quick misconfigurations as you can perform most of this tests with automated tools

    Services Enumeration

        You probably won't find much more misconfigurations here if you performed correctly the benchmark tests, but you might find some that weren't being looked for in the benchmark test.

        This will allow you to know what is exactly being used in the cloud env

        This will help a lot in the next steps

    Check exposed assets

        This can be done during the previous section, you need to find out everything that is potentially exposed to the Internet somehow and how can it be accessed.

            Here I'm taking manually exposed infrastructure like instances with web pages or other ports being exposed, and also about other cloud managed services that can be configured to be exposed (such as DBs or buckets)

        Then you should check if that resource can be exposed or not (confidential information? vulnerabilities? misconfigurations in the exposed service?)

    Check permissions

        Here you should find out all the permissions of each role/user inside the cloud and how are they used

            Too many highly privileged (control everything) accounts? Generated keys not used?... Most of these check should have been done in the benchmark tests already

            If the client is using OpenID or SAML or other federation you might need to ask them for further information about how is being each role assigned (it's not the same that the admin role is assigned to 1 user or to 100)

        It's not enough to find which users has admin permissions "*:*". There are a lot of other permissions that depending on the services used can be very sensitive.

            Moreover, there are potential privesc ways to follow abusing permissions. All this things should be taken into account and as much privesc paths as possible should be reported.

    Check Integrations

        It's highly probably that integrations with other clouds or SaaS are being used inside the cloud env.

            For integrations of the cloud you are auditing with other platform you should notify who has access to (ab)use that integration and you should ask how sensitive is the action being performed.
            For example, who can write in an AWS bucket where GCP is getting data from (ask how sensitive is the action in GCP treating that data).

            For integrations inside the cloud you are auditing from external platforms, you should ask who has access externally to (ab)use that integration and check how is that data being used.
            For example, if a service is using a Docker image hosted in GCR, you should ask who has access to modify that and which sensitive info and access will get that image when executed inside an AWS cloud.

Multi-Cloud tools

There are several tools that can be used to test different cloud environments. The installation steps and links are going to be indicated in this section.

PurplePanda https://github.com/carlospolop/purplepanda 

A tool to identify bad configurations and privesc path in clouds and across clouds/SaaS.

# You need to install and run neo4j also
git clone https://github.com/carlospolop/PurplePanda
cd PurplePanda
python3 -m venv .
source bin/activate
python3 -m pip install -r requirements.txt
export PURPLEPANDA_NEO4J_URL="bolt://neo4j@localhost:7687"
export PURPLEPANDA_PWD="neo4j_pwd_4_purplepanda"
python3 main.py -h # Get help

Prowler https://github.com/prowler-cloud/prowler 

It supports AWS, GCP & Azure. Check how to configure each provider in https://docs.prowler.cloud/en/latest/#aws

# Install
pip install prowler
prowler -v

# Run
prowler <provider>
# Example
prowler aws --profile custom-profile [-M csv json json-asff html]

# Get info about checks & services
prowler <provider> --list-checks
prowler <provider> --list-services

CloudSploit https://github.com/aquasecurity/cloudsploit 

AWS, Azure, Github, Google, Oracle, Alibaba

# Install
git clone https://github.com/aquasecurity/cloudsploit.git
cd cloudsploit
npm install
./index.js -h
## Docker instructions in github

ScoutSuite https://github.com/nccgroup/ScoutSuite 

AWS, Azure, GCP, Alibaba Cloud, Oracle Cloud Infrastructure

mkdir scout; cd scout
virtualenv -p python3 venv
source venv/bin/activate
pip install scoutsuite
scout --help
## Using Docker: https://github.com/nccgroup/ScoutSuite/wiki/Docker-Image
