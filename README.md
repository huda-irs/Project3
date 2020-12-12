# Project3 - Replicate SincNet Results

[SincNet repo](https://github.com/huda-irs/Project3/blob/main/SincNet.png)

DISCLAIMER: I do not take credit for the repositorty and the image above that describes the porject. This is not my creation. The purpose of this repoistory was to recreate its results and understand the CNN portion of the repoisotry. All credit is given the the orginal owners of the repository which can be found at [mravanelli/SincNet](https://github.com/mravanelli/SincNet)

# Reason
This Project recreated results from the [SincNet repo](https://github.com/mravanelli/SincNet). The SincNet repo was executed for its unique technique for training the machine to filter out data. Although SincNet is a full network, a CNN model that feeds into a DNN model and then feeds into another DNN model that classifies the speaker, the focus on this project the is CNN portion of the repository.

# How SincNet CNN works
SincNet uses CNN to filter out a signal efficiently. The SincNet model takes the signal and segments using the sliding window technique. Taking 200 samples per segments and the difference between on segment and the consecutive segment is the 5 samples that are slid over for the next window. 

![sliding window segmentation](https://github.com/huda-irs/Project3/blob/main/sliding_window.png)

Figure: Visual as to how the data is segmented into parts. The image can be found the source [here](https://stackoverflow.com/questions/55874826/feature-extraction-for-keyword-spotting-on-long-form-audio-using-a-cnn)

These segments are then fed into the CNN network in batches. This is important becuase the intentional choice of training the machine with large batches is important becuase large batch sizes makes training efficient in time and assists in overcoming the issue of overfitting the model. THe batch normalization layer is only possible for large batch sizes and greatly impacts the performace of the machine for the reasons mentioned for the large batch sizes.

![batch layer normalization](https://github.com/huda-irs/Project3/blob/main/batch_normalization.jpeg)

Figure: Visual for batch normalization layer. From the image shown, it makes sense as for the use of large batch sizes. The batch normalization larger would not be as effective with small batch sizes. The trade off that is faced with large batche sizes is good performance (larger batch size) and memory space (reason we can't have extremely unreasonable size for batch sizes). The image above can be found by its source [here](https://medium.com/deep-learning-g/batch-normalization-af993b5d58b1)

SincNet's CNN portions has each batch pass through the SincConv_fast class once and then loops that output computes 1D convolution twice more. The difference between the 1D convolution and the 1D convolution from the SincConv_fast class are the filter lengths, number of filters, and input. The SincConv_fast class first processes the segmented signal batches proved and then provides the processed data into the other 1d convolutional neural networks. The processing is does by 3 band pass filtering. The band pass filtering is important for the processing becuase it's effectiviness will impact the model in the DNN processing as well. The reason for this is because the processing reduces noise and unwanted signals from the raw audio which will reduce the model's influence on these imperfections in the raw signal. The processed signal is then processed by the 1D convultional neural network with the filters in the SincConv_fast class and then a normal 1D convolution without the filters twice. The result of the batch after convolving the signal 3 times is then fed into the CNN model. That output is then passed the the DNN model and so forth to classify the speaker. 

![1D Convolution](https://github.com/huda-irs/Project3/blob/main/1DConv.jpg)

Figure: Visual representation of 1 dimension convolution. The video in which the 1D convolution image is extracted from can be found [here](https://www.youtube.com/watch?app=desktop&v=TYPnBOEzq9o) 

# How is it efficient

[1] Does not require as many outputs as other machine learning techiques for filtering because it only outputs the start and stop frequencies for filtering

[2] Since the data is segmented SincNet can detect frequencies to filter out sooner than most models

Results:

My results from training the model can be found under exp/SincNet_TIMIT/my_model_run.res file. The results from the creators of SincNet are also available under exp/SincNet_TIMIT/orginalModel.res. From comparison of the two models, it is shown that my run of the resulted higher loss and error values for each epoch in comparison to the creators. I believe the difference may be because of the type of GPU being used. The creators of SincNet states their network was trainedon an NVIDIA TITAN X. In my cause, it is unsure of the exact gpu. The GPU I used is an NVIDIA gpu but is not the TITAN X gpu.
