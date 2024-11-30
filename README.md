# SEEG FMRI on music

SEEG subject list: s011, s012, s013, s014, s015, s022, s023, s024, s025, s026, s031, s034, s035, s036, s038, s039, s047, s048, s050, s051, s054

** all subjects used 2048 Hz sampling rate; except s013 and s015 used 512 Hz sampling rate.

## SEEG electrode processing
- get electrode data and calculate TFR: get_seeg_tfr_hrf_sxxx_110824.m
  'sxxx' are codes for each subject
- "average" TFR across subjects: get_seeg_tfr_multiple_avg_111724.m
  This script selected electrodes around A1 (15 mm to the centroid of either left or right A1) and average their data
  ```
  file_seeg_tfr={
        'seeg_tfr_hrf_s050_110824.mat'; %lh 3.2 mm to A1
        'seeg_tfr_hrf_s011_110824.mat'; %lh 5.0 mm to A1
        'seeg_tfr_hrf_s026_110824.mat'; %lh 6.2 mm to A1
        %'seeg_tfr_hrf_s022_110824.mat'; %lh 7.6 mm to A1
        'seeg_tfr_hrf_s012_110824.mat'; %lh 8.0 mm to A1
        'seeg_tfr_hrf_s014_110824.mat'; %lh 9.0 mm to A1
        'seeg_tfr_hrf_s048_110824.mat'; %lh 
        %'seeg_tfr_hrf_s024_110824.mat'; %lh 11.4 mm to A1
	    %'seeg_tfr_hrf_s034_110824.mat'; %rh 4.4 mm to A1
        'seeg_tfr_hrf_s038_110824.mat'; %rh 4.7 mm to A1
        'seeg_tfr_hrf_s051_110824.mat'; %rh 4.8 mm to A1
        'seeg_tfr_hrf_s054_110824.mat'; %rh 7.4 mm to A1
        'seeg_tfr_hrf_s047_110824.mat'; %rh 10.2 mm to A1
        'seeg_tfr_hrf_s036_110824.mat'; %rh 10.9 mm to A1
        'seeg_tfr_hrf_s031_110824.mat'; %rh 
        'seeg_tfr_hrf_s039_110824.mat'; %rh 
    };

ch_select={
    [58 59 60 61 57];      %s050; T2, T3, T4, T5
    [108 109 110 111 112 71 72];  %s011; T1, T2, T3, T4
    [64 65 66 63 67 93];         %s026; T3, T4, T5
    %[];                %s022; B6, no data
    [32 33 34 31 35];         %s012; T3, T4, T5
    [46 47 44 45 48 62 63];            %s014; T3, T4
    [39 40 41];         %s048;
    %[];                %s024; Y1, no data
    %[];                %s034; T'5, : data
    [42 43 44 45];         %s038; T'1, T'2, T'3
    [27 28 29 30 26 31];      %s051; T'2, T'3, T'4, T'5
    [71 72 66 67];               %s054; T'4, T'6
    [73 72 74 75];              %s047; T'2
    [37 36 38 39 40 29];              %s036; T'3
    [40];                           %s031;
    [75 76 77];                     %s039;
    };
    
```
    output: seeg_tfr_multiple_avg_111724.mat tfr_s tfr_v freqVec

## SEEG source processing
- get electrode data: `prepare_seeg_091924.m` and `prepare_seeg_ncov_091924.m` in all subjects
- source modeling:
  - make_bem_d10_wb_dec_091924.m: create BEM
  - make_fwd_openmeeg_091924.m: calculate forward solution
  - make_seeg_fwd_wb_dec_091924.m: collect forward solution
  - make_dec_wb_mne_102224.m: MNE
  - calc_dec_wb_mne_roi_102224.m: collect source modeling results at ROIs
 
- Entrainment: correlation between acoustics and SEEG signals:
  - electrode_entrain_env_091924.m: correlate acoustic envelop with SEEG signals
  - electrode_entrain_env_freq_091924.m: correlate frequency components of the acoustic envelop with SEEG signals
    
