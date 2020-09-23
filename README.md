This project aims to create a quantum-classical hybrid classifier for the detection of COVID-19 from lung CT scans. The starting point was a survey of current AI methods in quantum computing, both gate based and annealing based. Methods that were close to practical applications were identified. A Quantum Assisted Helmholtz Machine (Based on the work of Benedetti et al.) was implemented. This is a sampling-based neural network where the classical and quantum layers work together to train an unsupervised generative model. This was implemented using D-Wave’s quantum annealer, which is very efficient as a sampler. MNIST handwritten digits were used to train the network. After training with a Wake-Sleep Algorithm, the network produced remarkable results where the nearest neighbor of the generated image in the training set was very close to the generated image. 

Work then proceeded by surveying existing classical methods for accurate COVID-19 diagnosis from CT scans. In the work of Zhang et al. , they use a two-fold method consisting of an image segmentation network (DeepLabv3) and a classification network (3DResNet-18). A raw CT scan image is first passed through the segmentation network to identify lesions (Ground Glass Opacity, Consolidation, etc) and label them. Labeled images are given as an input to the classification network to obtain the final diagnosis. (COVID Pneumonia vs Common Pneumonia vs Healthy)

This idea was adopted by using a quantum classification algorithm (QBoost - based on the work of Neven et al) in place of the classical classifier. This quantum algorithm uses an ensemble of weak classifiers whose ensemble weights are determined from the quantum processor by creating a loss function compatible with optimization on the D-Wave quantum computer.

Open source annotated CT scan images were then used to train a segmentation network that labeled the image pixels as background, pulmonary regions, and lesions. ([This work by Luke Cao was used](https://github.com/cadae/COVID-19-Infection-CT-Scan-Images-Segmentation)). The segmented output was passed through the quantum classifier. QBoost achieved a 70% test accuracy in classifying Normal Lung Scans from Pneumonia infected lung scans and a 67% test accuracy in classifying COVID-19 Lung Scans from Common Pneumonia lung scans. 

Current work is focused on using improved classical segmentation networks which provide a larger number of labels (this provides more data about the specific kinds of lesions present). The hyperparameters in the quantum classifier, like the number of weak classifiers, the annealing time, etc. are also being tuned. The relationship between a larger number of qubits and better accuracy in classification is also being investigated. 
