# Project3 - Replicate SincNet Results

# Reason
This Project recreated results from the [SincNet repo](https://github.com/mravanelli/SincNet). The SincNet repo was executed for its unique technique for training the machine to filter out data. 

# How SincNet CNN works
SincNet uses CNN to filter out a signal efficiently. The SincNet model 

# How is it efficient

[1] Does not require as many outputs as other machine learning techiques for filtering because it only outputs the start and stop frequencies for filtering
[2] Since the data is segmented SincNet can detect frequencies to filter out sooner than most models

Results:

My results from training the model can be found under exp/SincNet_TIMIT/my_model_run.res file. The results from the creators of SincNet are also available under exp/SincNet_TIMIT/orginalModel.res. From comparison of the two models, it is shown that my run of the resulted higher loss and error values for each epoch in comparison to the creators. I believe the difference may be because of the type of GPU being used. The creators of SincNet states their network was trainedon an NVIDIA TITAN X. In my cause, it is unsure of the exact gpu. The GPU I used is an NVIDIA gpu but is not the TITAN X gpu.
