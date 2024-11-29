# SEEG FMRI on music

SEEG subject list: s011, s012, s013, s014, s015, s022, s023, s024, s025, s026, s031, s034, s035, s036, s038, s039, s047, s048, s050, s051, s054

** all subjects used 2048 Hz sampling rate; except s013 and s015 used 512 Hz sampling rate.

## SEEG processing
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
