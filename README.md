# AdaptiveMomentum
### Training an artificial neural network with an adaptive momentum using a fuzzy inference system

An interactive algorithm for the optimization of momentum in the SGD optimizer is designed. During the training process of the artificial neural network, after the completion of each epoch, this algorithm takes in the loss values for training and validation, and after 3 epochs (modifiable by the AVG variable) the average of the losses during the 3 epochs is calculated and compared to the previous average value. The difference between the two average values for both training and validation losses are used as the input for the fuzzy inference system (FIS). The output of the FIS is the necessary change in momentum.

The output of the FIS is a value between -1 and 1. If we take this value as x, the value of the momentum is multiplied by 10<sup>x</sup>. Which means that if x<0, the momentum will decrease and if x>0, it will increase. However, an upper limit of 0.9 is set for the momentum.

The FIS has two inputs; Training Loss (TL) variation and Validation Loss (VL) variation, and the output is a criterion for change in the Momentum (M). For the output and each of the inputs, three membership functions have been used, which represent Increase (I), Decrease (D), and No Change (NC). Using the abbreviations, the following are the rules of the FIS:

![image](https://user-images.githubusercontent.com/65850584/224509462-3c62f077-9135-46bd-b834-d7760ed25cda.png)

This algorithm has been used to train a fully-connected artificial neural network on the Fashion MNIST dataset. In order to gain the best possible results, 20 different network designs with different hyperparameters were tried and the best performing one was chosen. This network has 4 hidden layers, each with 30 neurons and PReLU activation functions. The optimizer is SGD,  the learning rate is 0.001, and the initial momentum is 0.3. Categorical cross-entropy has been used as the loss function and the training was done in 50 epochs. Also, 20% of the whol data was used as test data, and out of the remaining 80%, another 20% was used as validation data.

After training, the accuracy of the network by evaluation on the test data was 86.94%. In order to compare this result to a network trained with a constant momentum, the same network was trained on multiple tests with different values of momentum, out of which, the best results were gained by a momentum of 0.3 with a test data accuracy of 85.41%.

In addition to a better accuracy compared to the fixed momentum, the proposed algorithm showed less oscilation of loss and accuracy during training as well. In order to compare these oscillations, the following figures demonstrate the cahnges of loss and accuracy values for the two tested methods of training.

![image](https://user-images.githubusercontent.com/65850584/224510182-28cbc670-a97f-463d-956c-e32e702af94c.png)

Changes of accuracy in the training and validation data by using the adaptive momentum


![image](https://user-images.githubusercontent.com/65850584/224510212-a5044ecb-51fc-4c3d-b0db-1a3b5da6d579.png)

Changes of accuracy in the training and validation data by using a constant momentum


![image](https://user-images.githubusercontent.com/65850584/224510231-8ca3143b-f5da-43a5-9af0-1c749dc3068b.png)

Changes of loss in the training and validation data by using the adaptive momentum


![image](https://user-images.githubusercontent.com/65850584/224510244-53a1f8e6-ffe4-4ebb-ba9a-dcd708ad1d98.png)

Changes of loss in the training and validation data by using a constant momentum
