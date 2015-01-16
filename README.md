# RRI_estimation
MATLAB: Generates R-R interval (RRI) data from raw ECG data

Cardiac output is typically recorded in the form of ECG which contains several clearly identifiable peaks. In particular, the R peaks are dominant sharp peaks in the waveform. Most analysis is performed on a time series derived from the ECG – the RR interval (RRI) – which is the time difference between consecutive R peaks.

The RRI is obtained via the following steps:
 
Step 1: The ECG is bandpass filtered (suggested range 5 - 20 Hz)

Step 2: The R peaks are estimated. R peaks are expected to be larger than parameter 'ampthresh', and it is expected that a minimum time interval exists between successive peaks 'timethresh'.

Step 3: The user is presented with a plot illustrating peaks that have been identified (upper subplot) and the time difference between  successive peaks (lower subplot). The user is then prompted with: 
 
           Change parameters (Y/N) ?

Entering 'Y' allows the user to change the parameters before proceeding to the next step. If only a small number of peaks have been misclassified (anomalies), the user may review these errors in the next step by entering 'N'.
 
Step 4: If anomalies have been detected, the user is then prompted with:
 
           Possible anomaly detected on or after time x, remove (Y/N)? 
 
For each detected anomaly, the user can then manually review the plots to determine whether the anomaly is genuine (a peak has not been detected OR a spurious peak has been detected). If the anomaly is genuine, the user should enter 'Y' and the anomaly will be corrected. Otherwise, the user should enter 'N' and no changes will be made concerning the potential anomaly. The sensitivity of the anomaly detection algorithm is controlled by 'anomalyparam'.

Step 5: The difference between R peaks is sampled at regular intervals (controlled by parameter fsRRI) to generate the RRI.

Step 6: The user is presented with a plot of the final RRI with detected anomalies, and a plot of the RRI with anomalies removed. 

 -------------------------------------------------------------------------
 Required inputs:
 
       xECG  ~  An ECG time series. The expected voltage range is microvolt.
                At least 5 s of ECG is required to estimate the RRI.
       fsECG ~  The sampling frequency of the ECG. Recordings with
                sampling frequencies below 32 Hz will be rejected.
 
 -------------------------------------------------------------------------
 Outputs:
 
       xRRI  ~  The RR interval (RRI) time series, sampled at regular
                intervals.
       fsRRI ~  The sampling frequency of the RRI.
 
-------------------------------------------------------------------------
 Parameters:
 
       Hp             ~    High pass ECG filter cutoff (in Hz).
       Lp             ~    Low pass ECG filter cutoff (in Hz).
       ampthresh      ~    Minimum R peak amplitude.
       ampthresh_autodetect ~ 'Y' (default) or 'N'. The user can let the function 
                           pick an appropriate value for 'ampthresh'.   
       timethresh     ~    Minimum time distance between R peaks (in s). 
       fsRRI          ~    The sampling frequency of the RRI.
       anomalyparam   ~    Controls the sensitivity of the anomaly detection
                           algorithm. The larger the value, the less
                           sensitive the algorithm.
           
 
Parameter values can be changed from their default values in the following way:

	[xRRI,fsRRI]=ECG_to_RRI(xECG,fsECG,'timethresh',0.5);
 
In the above, the user has selected the parameter 'timethresh' as 0.5 s. 
