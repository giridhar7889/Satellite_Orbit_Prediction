<div align="center">

# Satellite Orbit Prediction Using Machine learning approach Project

</div>

<!-- <div align="center" height=60px width=60px>
<img src="https://github.com/furiousMAC/continuity/blob/master/figs/fp.png" alt="A dolphin shooting WiFi from an Uzi" height="120">
</div> -->

Our knowledge of space weather and
air density is limited, trajectories are only seldom obtained from noisy ground-based radar systems, and
satellite operators are reluctant to disclose their maneuvering intentions. Current orbit predictions that
are only based on physics-based models may not achieve the required accuracy for collision avoidance
and have already resulted in satellite collisions due to the lack of information regarding the state of the
space environment and resident space objects’ (RSOs’) body characteristics. Two line element sets(TLE)
made accessible to the public lack any related error or correctness information. The majority of TLE
prediction techniques used today fit polynomials, which cannot capture periodic properties. This paper
has presented a methodology for orbital prediction using curve fitting and LSTM on historical orbital
data. The proposed machine learning approaches are used with various TLE parameters where the LSTM
model is trained to learn through large amounts of historical TLE data. The fitted data is synthesized
and then compared with the SGP4 predictions. The two proposed methods focus on reducing prediction
errors. The results of the study demonstrate that the proposed machine learning approaches can improve
orbital prediction accuracy with good performance in most cases. We go into further optimization and
the computing needs for using all-on-all conjunction analysis on the whole TLE collection and visualize
when and where conjunction may occur, both currently and in the near future.

This project aims to be an experimental playground for using Machine learning to limit error in orbit prediction and prime contributions are listed below:

- Using LSTM and curve fitting for making predictions of satellite’s TLE (The proposed ML
  approach orbit is closer to the true orbit).
- Obtaining a comparable accuracy to the SGP4 model.
- Train and use machine learning models to learn the error in orbit prediction models.
- The distinctive study that we have performed to predict new data parameters in base on the
  data we had with comparable accuracy and limiting error in such prediction
- The machine learning model’s projected TLEs can accurately determine the
  reference orbit.

<!--
- <a href="messages/airprint.md">AirPrint Message</a>
- <a href="messages/airdrop.md">AirDrop Message</a>
- <a href="messages/homekit.md">HomeKit Message</a>
- <a href="messages/proximity_pairing.md">Proximity Pairing Message</a>
- <a href="messages/hey_siri.md">"Hey Siri" Message</a>
- <a href="messages/airplay_target.md">Airplay Target Message</a>
- <a href="messages/airplay_source.md">Airplay Source Message</a>
- <a href="messages/magic_switch.md">Magic Switch Message</a>
- <a href="messages/handoff.md">Handoff Message</a>
- <a href="messages/tethering_target.md">Tethering Target Message</a>
- <a href="messages/tethering_source.md">Tethering Source Message</a>
- <a href="messages/nearby_action.md">Nearby Action Message</a>
- <a href="messages/nearby_info.md">Nearby Info Message</a>
- <a href="messages/findmy.md">Find My Message</a>  -->

## Prerequisites

Python 3 (>=3.5) is required to run the code. We also recommend using
[virtualenv](https://virtualenv.pypa.io/en/stable/) for isolated Python environments and
[pip](https://pypi.org/project/pip/) for package management. Note, to create a Python 3 environment you need to run:

```
virtualenv .env --python=python3
source .env/bin/activate
```

The code also assumes that [PyTorch](https://pytorch.org/) is already installed.

## Models and Datasets

Dataset:-
A two-line element set (TLE) is a standardized
format for describing a satellite’s orbit and trajectory. Below is an example of the International
Space Station. There are 14 fields in a TLE; however, our method only needs 9 of them.The orbits
of tracked RSOs around Earth are specified and updated in the US space catalog as TLEs. TLE
data is readily available for satellite owners and operators at Space-Track.Org published by US
strategic command (USSTRATCOM).
<a href="messages/findmy.md">Space Track .org</a>

Models-LSTM:-
Long short-term memory, LSTM algorithm, which is a type of Recurrent Neural Network (RNN).
An input layer, a hidden layer, and an output layer make up the three layers. By constructing
weight coefficients between hidden layers, LSTM solves the problem of long-distance dependence
that RNNs cannot manage. It indicates that while forecasting satellite telemetry parameter time
series data, LSTM can develop long-term connections between distant nodes in the time series,
improving the accuracy of time series data prediction.
Our intuition to use LSTM was because of its effectiveness on the time series. We have only
used linear regression in some cases where data looked linear. Looking closely at the linear
data points, one would notice they usually return back to a value after some time abruptly.
Like a modulo operation so delinearize helps with taking a linear result and applying a modulo
operation to the result.

To modify each epoch weight and the loss function efficiently, we have used the Adamax optimizer,
a variant of Adam based on the infinity room . As this problem is large in terms of data
parameters, the Adam optimizer is a primary algorithm for optimization to estimate lower-order moments.
Training the model would continue by comparing the output with the target, calculating
the error, and optimizing the weights, reiterating the process again and again. We believe that
we did a thorough hyper-parameter search and optimization in order to seek the best overall
parameters in order to minimize our loss on the validation set.
We have also chosen an ideal number of epochs after which the accuracy stopped increasing.
When determining optimized weights for the trained model, the loss function is the most
important factor to consider. The MAE loss function is used as it is more robust to outliers. This
fully-connected neural network learns the mapping between the input and output by connecting
all neurons available, and it has 201,052,641 trainable parameter.

Models -Curve Fitting:-

The linear or non-linear curve fitting method is a mere global minimization of the weighted
sum of squares. So in our study, for some parameters such as the right ascension of the node, the
argument of perigree, mean anomaly, eccentricity, the weighted sum of squares, and root mean
squared error is used to assess the goodness of fit. TLE data is input to either adjust a smooth
and balancing model function that describes the data adequately or train a special kind of
recurrent neural network that is capable of learning long-term dependencies in data.

## Citations

- [H. Peng, X. Bai, Improving orbit prediction accuracy through supervised machine learning,Advances in Space Research 61 (2018) 2628–2646 ](https://www.researchgate.net/publication/322518105_Improving_Orbit_Prediction_Accuracy_through_Supervised_Machine_Learning)

- [C. Levit, W. Marshall, Improved orbit predictions using two-line elements, Advances in Space Research 47 (2011) 1107–1115](https://www.researchgate.net/publication/222413947_Improved_orbit_predictions_using_two-line_elements?enrichId=rgreq-877bbc3acbea196c9fb857cfc5493e83-XXX&enrichSource=Y292ZXJQYWdlOzIyMjQxMzk0NztBUzo3NTE2NDMxMzgyMjQxMjlAMTU1NjIxNzA5Nzk0Mg%3D%3D&el=1_x_2&_esc=publicationCoverPdf)

- [H. Peng, X. Bai, Comparative evaluation of three machine learning algorithms on improving orbit prediction accuracy, Astrodynamics 3 (2019 325–343.](https://link.springer.com/article/10.1007/s42064-018-0055-4)

- [R. Abay, S. Balage, M. Brown, R. Boyce, Two-line element estimation using machine learning, The Journal of the Astronautical Sciences 68 (2021) 273–299.](https://www.researchgate.net/publication/328353548_Two-Line_Element_Estimation_Using_Machine_Learning)

- [C. Puente, M. A. Sáenz-Nuño, A. Villa-Monte, J. A. Olivas, Satellite orbit prediction using big data and soft computing techniques to avoid space collisions, Mathematics 9 (2021) 2040](https://www.mdpi.com/2227-7390/9/17/2040)

- [Machine Learning Approach to Improve Satellite Orbit Prediction Accuracy Using Publicly Available Data](https://www.researchgate.net/publication/333100021_Machine_Learning_Approach_to_Improve_Satellite_Orbit_Prediction_Accuracy_Using_Publicly_Available_Data?enrichId=rgreq-e456370920f8f254fbb1c870673667a3-XXX&enrichSource=Y292ZXJQYWdlOzMzMzEwMDAyMTtBUzoxMDExODkzNDE0MTQ2MDQ5QDE2MTgyNjU1OTgyOTk%3D&el=1_x_2&_esc=publicationCoverPdf)
