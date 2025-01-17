# DevOps and SRE
- Focus on automation
- Failure is normal
- Reframe of 'availability' to what the business can tolerate.

### DEvOps Paradigm
Delivering perfection is nearly impossible. So aim at the agreed upon objectives!!
#### SLO
Service Level Objectives
### SLI
Service Level Indicators = metrics
The indicators should map to the practical reality of the service delivery

## Basic automation scripting
- Bash scripting
- sdk's
#### Procedural automation
- Is an ordered list of command that will be executed to achieve a goal.

Examples of this method
- Python SDK's

#### The declarative automation
Instead of telling which steps should be executed and in a specified order, you just define in a configuration file how the infrastructure should look like. You DECLARE the end state.

Tools that use this type of programming are:
- Ansible
- puppet
- terraform