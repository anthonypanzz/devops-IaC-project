# CD12352 - Infrastructure as Code Project Solution
# Anthony Panzarella

## Spin up instructions
1. change directory (cd) to starter root
2. execute command- ./create.sh networkinfra network.yml network-paramters.json
3. when networkinfra stack is created, execute command- ./create.sh udagraminfra udagram.yml udagram-parameters.json to create second stack. 

## Tear down instructions
1. execute command- aws cloudformation delete-stack --stack-name udagraminfra
2. When network stack is deleted, execute command- aws cloudformation delete-stack --stack-name networkinfra

## URL verifying servers are running properly

![Screenshot 2025-03-02 124718](https://github.com/user-attachments/assets/24bb5ad4-0855-43eb-b69c-d4ed31413b1d)

---

![Screenshot 2025-03-02 124747](https://github.com/user-attachments/assets/5992a2eb-1904-47a6-926e-2956102605ed)
