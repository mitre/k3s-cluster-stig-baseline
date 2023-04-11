## K3S Cluster STIG Automated Compliance Validation Profile

InSpec profile to validate the secure configuration of a K3S Cluster against DISA's Kubernetes Secure Technical Implementation Guide (STIG) Version 1 Release 1.

## Kubernetes STIG Overview

The <b>Kubernetes</b> STIG (https://public.cyber.mil/stigs/) by the United States Defense Information Systems Agency (DISA) offers a comprehensive compliance guide for the configuration and operation of various technologies.
DISA has created and maintains a set of security guidelines for applications, computer systems or networks connected to the DoD. These guidelines are the primary security standards used by many DoD agencies. In addition to defining security guidelines, the STIG also stipulates how security training should proceed and when security checks should occur. Organizations must stay compliant with these guidelines or they risk having their access to the DoD terminated.

[STIG](https://en.wikipedia.org/wiki/Security_Technical_Implementation_Guide)s are the configuration standards for United States Department of Defense (DoD) Information Assurance (IA) and IA-enabled devices/systems published by the United States Defense Information Systems Agency (DISA). Since 1998, DISA has played a critical role enhancing the security posture of DoD's security systems by providing the STIGs. The STIGs contain technical guidance to "lock down" information systems/software that might otherwise be vulnerable to a malicious computer attack.

The requirements associated with the <b>Kubernetes</b> STIG are derived from the [National Institute of Standards and Technology](https://en.wikipedia.org/wiki/National_Institute_of_Standards_and_Technology) (NIST) [Special Publication (SP) 800-53, Revision 4](https://en.wikipedia.org/wiki/NIST_Special_Publication_800-53) and related documents.

While the Kubernetes STIG automation profile check was developed to provide technical guidance to validate information with security systems such as applications, the guidance applies to all organizations that need to meet internal security as well as compliance standards.

## Getting Started

### Requirements

#### K3S Cluster
- K3S Platform deployment
- Access to the K3S Cluster API
- K3S Cluster Admin credentials cached on the runner.


#### Required software on the InSpec Runner
- git
- [InSpec](https://www.chef.io/products/chef-inspec/)

### Setup Environment on the InSpec Runner
#### Install InSpec
Goto https://www.inspec.io/downloads/ and consult the documentation for your Operating System to download and install InSpec.


#### Ensure InSpec version is at least 4.23.10 
```sh
inspec --version
```

#### Install InSpec Kubernetes Train
Kubernetes Train allows InSpec to send request over Kubernetes API to inspect the Kubernetes Cluster.

```sh
# Use one of the two following approaches for installing train-kubernetes.

# if InSpec was installed as a gem, use the system gem binary to install train-kubernetes.
# to check, compare `which inspec` to $GEM_HOME, if they match use
gem install train-kubernetes -v 0.1.6

# if InSpec was installed as a package, use the embedded gem binary to install train-kubernetes.
# to check, compare `which inspec` to $GEM_HOME, if they do not match or if $GEM_HOME is null use
sudo /opt/inspec/embedded/bin/gem install train-kubernetes -v 0.1.6

# Import gem as InSpec plugin
inspec plugin install train-kubernetes

#If it has the version set to "= 0.1.6", modify it to "0.1.6" and save the file.
vi ~/.inspec/plugins.json

# Run the following command to confirm train-kubernetes is installed
inspec plugin list
```
### How to execute this instance  
(See: https://www.inspec.io/docs/reference/cli/)

#### Validate access to Kubernetes API
```sh
kubectl get nodes

# Upon success try the following command to validate InSpec can reach the cluster API
inspec detect -t k8s://
```

#### Execute a single Control in the Profile 
**Note**: Replace the profile's directory name - e.g. - `<Profile>` with `.` if currently in the profile's root directory.

```sh
inspec exec <Profile> -t k8s:// --controls=<control_id> <control_id> --reporter cli
```

#### Execute a Single Control and save results as JSON 
```sh
inspec exec <Profile> -t k8s:// --controls=<control_id> <control_id> --reporter json:results.json
```

#### Execute All Controls in the Profile 
```sh
inspec exec <Profile> -t k8s:// --reporter cli
```

#### Execute all the Controls in the Profile and save results as JSON 
```sh
inspec exec <Profile> -t k8s:// --reporter json:results.json
```

#### Execute all the Controls in the Profile and and see the results as they are run and save results as JSON 
```sh
inspec exec <Profile> -t k8s:// --reporter progress-bar json:results.json
```
