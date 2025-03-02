# CD12352 - Infrastructure as Code Project Solution
# Anthony Panzarella

## Spin up instructions
1. change directory (cd) to starter root
2. execute command- ./create.sh networkinfra network.yml network-paramters.json
3. when networkinfra stack is created, execute command- ./create.sh udagraminfra udagram.yml udagram-parameters.json to create second stack. 

## Tear down instructions
1. execute command- aws cloudformation delete-stack --stack-name udagraminfra
2. When network stack is deleted, execute command- aws cloudformation delete-stack --stack-name networkinfra

## Other considerations
TODO (optional)