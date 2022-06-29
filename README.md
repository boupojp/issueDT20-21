# Code 

# Submitted issue
Hi softmatterlab,

moving from DeepTrack (DT) 2.0 to 2.1 the generation of a sphere image presents some relevant differences.
DT 2.1 produces spheres that, fixing all the parameters except the z resolution in dt.Brightfield, changes dependently to the z resolution differently from DT 2.0.
This seems to originate to the upscale parameters in dt.Brightfield that in DT 2.1 doesn't work.

To check this you can run in Google Colab the notebook DeepTrackIssue.ipynb, https://colab.research.google.com/github/boupojp/issueDT20-21/blob/main/DeepTrackIssue.ipynb . If you choose in this notebook DT2.0 (setting oldversion = 1), you can see that, with upscale = 4, the z resolution doesn't affect the sphere image generation. Instead using upscale < 4, the z resolution affects the sphere image generation. In DT 2.1, the z resolution affects the sphere image generation with any value of upscale.
