# Active_Noise_Cancellation_Simulink

Goal of our ANC model is to remove all the sounds at a point (input). This is achieved  by actively cancelling all the noise by creating an audio which destructively interferes with it. 

# Components of the ANC
Functionality of different components used can be seen below

## Noise source:
  The noise source consists of “from multimedia” block. This is used to take a sound file as input. For files that are stereo, i.e., with 2 channels, "select columns" block is used which selects one of the 2 channels of the file input. This is because the ANC model is designed for mono files.
  
## Primary Path and Secondary path::
  The primary path represents the transfer function for the sound in its primary path. This will be the sound which we would hear without active cancellation. Similarly, the "estimated sec. path" represents the transfer function on secondary path. This is used to predict noise and estimate anti-noise. Both functions are polynomials and are adjusted by hit and trial to achieve cancellation on most of the sounds.
  The sound from secondary path is given as input to the LMS (least mean square) algorithm. The error, that is the sound heard which should have been suppressed, is given to the algorithm in addition. The algorithm calculates coefficients for LMS. The transpose of the output, the LMS coefficients vector is:
1)	Saved to the variable “simout”.
2)	Fed to the LMS filter copy. This generates the cancelling audio which is passed through the transfer function of the secondary path.
The summation of cancelling audio and audio from primary path gives the error which is fed to LMS algorithm. The error and primary sound are fed to a multiplexer to display simultaneously on single scope. A speaker is also attached to error sound.
