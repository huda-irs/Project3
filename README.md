# Project3 - Replicate SincNet Results

[SincNet repo](https://github.com/huda-irs/Project3/blob/main/SincNet.png)

DISCLAIMER: I do not take credit for the repositorty and the image above that describes the porject. This is not my creation. The purpose of this repoistory was to recreate its results and understand the CNN portion of the repoisotry. All credit is given the the orginal owners of the repository which can be found at [mravanelli/SincNet](https://github.com/mravanelli/SincNet)

# Reason
This Project recreated results from the [SincNet repo](https://github.com/mravanelli/SincNet). The SincNet repo was executed for its unique technique for training the machine to filter out data. Although SincNet is a full network, a CNN model that feeds into a DNN model and then feeds into another DNN model that classifies the speaker, the focus on this project the is CNN portion of the repository.

# How SincNet CNN works
SincNet uses CNN to filter out a signal efficiently. The SincNet model takes the signal and segments using the sliding window technique. Taking 200 samples per segments and the difference between on segment and the consecutive segment is the 5 samples that are slid over for the next window. 

![sliding window segmentation](https://github.com/huda-irs/Project3/blob/main/sliding_window.png)

These segments are then fed into the CNN network in batches. This is important becuase the intentional choice of training the machine with large batches is important becuase large batch sizes makes training efficient in time and assists in overcoming the issue of overfitting the model. THe batch normalization layer is only possible for large batch sizes and greatly impacts the performace of the machine for the reasons mentioned for the large batch sizes.

![batch layer normalization](https://github.com/huda-irs/Project3/blob/main/batch_normalization.jpeg)

SincNet's CNN portions has each batch pass through the SincConv_fast class once and then loops that output into the same 1D convolutionational neural network as SincNet twice. The difference between the 1D convolutional network and the 1D convolutional neutral network from the SincConv_fast class are the filter lengths, number of filters, and input. The SincConv_fast class first processes the segmented signal batches proved and then provides the processed data into the DNN network. 

# How is it efficient

[1] Does not require as many outputs as other machine learning techiques for filtering because it only outputs the start and stop frequencies for filtering
[2] Since the data is segmented SincNet can detect frequencies to filter out sooner than most models

Results:

My results from training the model can be found under exp/SincNet_TIMIT/my_model_run.res file. The results from the creators of SincNet are also available under exp/SincNet_TIMIT/orginalModel.res. From comparison of the two models, it is shown that my run of the resulted higher loss and error values for each epoch in comparison to the creators. I believe the difference may be because of the type of GPU being used. The creators of SincNet states their network was trainedon an NVIDIA TITAN X. In my cause, it is unsure of the exact gpu. The GPU I used is an NVIDIA gpu but is not the TITAN X gpu.
