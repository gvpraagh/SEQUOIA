# SEQUOIA
automated multiclass SEgmentation, QUantification, and visualizatiOn of the dIseased Aorta on hybrid PET/CT

<img src="Images/SEQUOIA_logo.jpg" width="720"/>

SEQUOIA is an automated pipeline for aortic PET/CT studies. First, it segments the ascending aorta, aortic arch, descending aorta, and abdominal aorta on low-dose CT from PET/CT. The multiclass segmentation is done using a 3D U-Net. Moreover, SEQUOIA provides tracer uptake values, calcium scores, background measurements, radiomic features, and a 2D visualization of the calcium and tracer distribution.

A CT scan can be used as input in niftii format. Based on this, the segmentation, calcium scores, and background measurement will be done. If the corresponding PET scan is given in niftii format too, the tracer uptake values and background measurements in PET will be given too. Make sure the PET is converted to wanted value: e.g., standardised uptake values (SUV), SUV normalized to lean body mass (SUL).

Please cite our article when you use SEQUOIA:
citation!

> Note: This is not a medical device and not intended for clinical usage. 

## Folder structure

For now it is only possible to run SEQUOIA with nifti (.nii or .nii.gz) files. Do make sure that the PET files are converted to the wanted quantification metric (SUV, SUL).
Your folder structure should look like this:

```
Data_folder
├── PT1
│   └── CT_pt1.nii
│   └── PET_pt1.nii (optional)
├── PT2
│   └── CT_pt2.nii
│   └── PET_pt2.nii (optional)
├── PT3
│   └── CT_pt3.nii
│   └── PET_pt3.nii (optional)
├── Etc...
```

The output will look like:
```
Data_folder
├── PT1
│   └── Output_folder
│       └── abd_aorta.nii
│       └── aorta.nii
│       └── aorta_combined.nii
│       └── arc_aorta.nii
│       └── asc_aorta.nii
│       └── asc_background.nii
│       └── data.csv
│       └── des_aorta.nii
│   └── CT_pt1.nii
│   └── PET_pt1.nii (optional)
├── PT2
│   └── Output_folder
│       └── abd_aorta.nii
│       └── aorta.nii
│       └── aorta_combined.nii
│       └── arc_aorta.nii
│       └── asc_aorta.nii
│       └── asc_background.nii
│       └── data.csv
│       └── des_aorta.nii
│   └── CT_pt2.nii
│   └── PET_pt2.nii (optional)
├── PT3
│   └── Output_folder
│       └── abd_aorta.nii
│       └── aorta.nii
│       └── aorta_combined.nii
│       └── arc_aorta.nii
│       └── asc_aorta.nii
│       └── asc_background.nii
│       └── data.csv
│       └── des_aorta.nii
│   └── CT_pt3.nii
│   └── PET_pt3.nii (optional)
├── Etc...
├── data.csv
```
Where abd = abdominal, arc = arch, asc = ascending, des = descending, aorta is the full aorta as one label, aorta_combined is the full aorta with four labels, and asc_background is the volume of interest in which the background measurements are done.
Per patient, a csv file is generated containing the SUV<sub>mean</sub>, SUV<sub>max</sub>, SUV<sub>peak</sub>, SUV<sub>sum</sub>, volume of the label, Agatston score, calcium volume, and calcium mass score per label.
Additionally, a data.csv file is generated in the main data folder with all data from every patient in the folder for easier comparisons.


## How to use

Usage is very easy. Make a virtual environment with your preferred Python notebook and install the required packages.
Tested with:
```
numpy == 1.25.0
tensorflow-gpu == 2.10.0
SimpleITK == 2.2.1
pandas == 2.0.3
opencv-python == 4.8.0.74
matplotlib == 3.7.2
scikit-image == 0.21.0
scikit-learn == 1.3.1
scipy == 1.11.1
pymeshfix == 0.16.2
meshio == 5.3.4
pyradiomics == 3.0.1
```

Then just run the program by:
```
python segmentation.py --data_dir "your\directory\here"
```

If you for example want to change the speed from accurate to fast, use:
```
python segmentation.py --data_dir "your\directory\here" --speed "fast"
```

You can also change the default settings in the _opts.py_ file. After that you can just run the _segmentations.py_ file.

> Note: do NOT change the last six arguments as these are settings for the model
