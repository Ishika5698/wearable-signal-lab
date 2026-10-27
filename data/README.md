# UCI HAR data for signal processing

These notebooks use the official UCI Human Activity Recognition Using Smartphones dataset: <https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones>.

Extract the official archive and place its `UCI HAR Dataset` directory here:

```text
data/raw/UCI HAR Dataset/
├── activity_labels.txt
├── train/y_train.txt
├── train/subject_train.txt
├── train/Inertial Signals/
│   ├── body_acc_x_train.txt
│   ├── body_acc_y_train.txt
│   ├── body_acc_z_train.txt
│   ├── total_acc_x_train.txt
│   ├── total_acc_y_train.txt
│   ├── total_acc_z_train.txt
│   ├── body_gyro_x_train.txt
│   ├── body_gyro_y_train.txt
│   └── body_gyro_z_train.txt
└── test/ (the matching labels, subject IDs, and nine signal files)
```

The notebooks first search this project's `data/raw/`, then parent folders, then a sibling `wearable-ai-101/data/raw/` folder. They can reuse that local copy without duplicating it. Raw and processed data are ignored by Git.
