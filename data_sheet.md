## Datasheet for Where's My Tabby?


### Motivation

- For what purpose was the dataset created? 
- Who created the dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)? Who funded the creation of the dataset?

- **Purpose**: Created to train an AI model for identifying an individual tabby cat (Mackenzie) from other tabby cats, as a proof-of-concept for lost pet recovery using photo-based AI. Supports capstone project for Imperial College AI certificate.
- **Creator**: dxunit-sam (personal/academic project).
- **Funding**: self-funded.

### Composition
- What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)? 
- How many instances of each type are there? 
- Is there any missing data?
- Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by    doctor–patient confidentiality, data that includes the content of individuals’ non-public communications)?

- **Instances**: Digital photos of cats (JPEG/HEIC format).
- **Number**: ~100+ (so far) photos of Mackenzie (user's cat); ~500 other tabby photos (balanced to ~300 for training).
- **Missing Data**: No.
- **Confidential Data**: No; Mackenzie photos are personal but non-confidential; other tabby photos are public from Kaggle (https://www.kaggle.com/datasets/ma7555/cat-breeds-dataset).

### Collection Process
- How was the data acquired? 
- If the data is a sample of a larger subset, what was the sampling strategy? 
- Over what time frame was the data collected?

- **Acquisition**: Mackenzie photos taken by me using iPhone 16 Pro in varied lighting, angles, and postures. Other tabby photos downloaded from Kaggle Cat Breeds Dataset and filtered for tabby breeds.
- **Sampling**: Random sampling for other tabbies; reduced to 500 via Terminal command for balance.
- **Time Frame**: Mackenzie photos: July-August 2025; Kaggle data: As per dataset upload.

### Preprocessing/Cleaning/Labelling
- **Preprocessing**: Converted to RGB, center-cropped to square preserving proportions, resized to 224x224, augmented with random rotations/crops for training. Labels: Binary (1 for Mackenzie, 0 for others).
- **Raw Data Saved**: Yes; original photos retained in local folders.

### Uses
- **Other Tasks**: Pet breed classification, lost pet matching apps, general animal recognition models.
- **Impact on Uses**: Limited to tabby cats; may underperform on non-tabby or low-pattern breeds (e.g., solid black/white cats). Consumers should augment data for diversity to mitigate bias or unfairness (e.g., inaccurate identification leading to false positives in recovery apps).
- **Tasks Not to Use**: High-stakes applications (e.g., legal or security identification); commercial use without permission.

### Distribution
- **Distributed**: Via GitHub repo (https://github.com/dxunit-sam/wheres-my-tabby); structure shared, but personal photos not uploaded.
- **License/ToU**: Kaggle data under CC BY-NC-SA 4.0; Mackenzie photos for educational use only, no explicit license.

### Maintenance
- **Maintainer**: dxunit-sam (project creator); updates via GitHub issues/PRs.## Datasheet for "Where's My Tabby?" Dataset

### Motivation

- For what purpose was the dataset created?  
  The dataset was created to train and test an AI model for identifying an individual tabby cat (Mackenzie) from other tabby cats, as a proof-of-concept for lost pet recognition using photos. This serves as the capstone project for the Professional Certificate in Machine Learning and Artificial Intelligence at Imperial College.

- Who created the dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)? Who funded the creation of the dataset?  
  Created by dxunit-sam (the project owner) as part of their individual capstone project at Imperial College. No external funding; self-funded through personal resources and course participation.

### Composition

- What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?  
  The dataset consists of RGB photos of cats: one class for Mackenzie (the owner's cat) and another for other tabby cats.

- How many instances of each type are there?  
  - Mackenzie: ~300 photos.  
  - Other tabby cats: ~500 photos (sampled from larger set).  
  Total: ~800 photos.

- Is there any missing data?  
  No missing data; all images are complete and labeled.

- Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor–patient confidentiality, data that includes the content of individuals’ non-public communications)?  
  No; Mackenzie photos are the owner's personal images (non-confidential), and other tabby photos are from a public Kaggle dataset.

### Collection process

- How was the data acquired?  
  - Mackenzie photos: Taken by the owner using an iPhone 16 Pro, focusing on varied angles, lighting, and postures.  
  - Other tabby photos: Downloaded from Kaggle Cat Breeds Dataset (filtered for tabby breeds like American Shorthair Tabby).

- If the data is a sample of a larger subset, what was the sampling strategy?  
  Other tabby photos were randomly sampled from the Kaggle dataset (original ~3,000+ images) down to 500 using a Terminal command (`find images/OtherTabby -type f | sort -R | tail -n +501 | xargs -I {} rm -v {}`), then further sampled to 300 for balance.

- Over what time frame was the data collected?  
  Mackenzie photos: Collected in August 2025 (ongoing).  
  Other tabby photos: Sourced from Kaggle dataset (collection timeframe unknown, likely pre-2023).

### Preprocessing/cleaning/labelling
- Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)? If so, please provide a description. If not, you may skip the remaining questions in this section.  
  Yes:  
  - Converted HEIC/JPG to RGB using PIL.  
  - Resized to 224x224 with proportion-preserving center cropping and Lanczos resampling.  
  - Augmented with random rotations (0-360°), flips, and brightness adjustments.  
  - Labeled binary: 1 for Mackenzie, 0 for other tabbies.  
  - Balanced classes by sampling; no missing values removed (none present).

- Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?  
  Yes; original photos are preserved in the `images/Mackenzie` and `images/OtherTabby` folders.


### Uses

- What other tasks could the dataset be used for?  
  - Pet breed classification or general animal recognition.  
  - Training models for lost pet matching apps.  
  - Augmenting larger datasets for computer vision research on fur patterns.

- Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses? For example, is there anything that a dataset consumer might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other risks or harms (e.g., legal risks, financial harms)? If so, please provide a description. Is there anything a dataset consumer could do to mitigate these risks or harms?  
  - Composition bias: Focused on tabby cats, may underperform on non-tabby breeds (e.g., solid-colored cats with fewer patterns). Personal photos are from one cat, limiting diversity.  
  - Preprocessing: Random rotations and crops could distort features if not reapplied carefully.  
  - Risks: Potential misidentification in real-world apps (e.g., false positives leading to incorrect owner notifications). Legal risks if used for surveillance without consent.  
  - Mitigation: Augment with diverse breeds; test on validation sets; ensure ethical use (e.g., opt-in databases); add disclaimers for non-commercial applications.

- Are there tasks for which the dataset should not be used? If so, please provide a description.  
  - Surveillance or tracking without consent (privacy violations).  
  - Commercial applications without licensing Kaggle data or my permission.  
  - This model is not yet proven in use in reality, using this model for your own risk.


### Distribution
- How has the dataset already been distributed?  
  Shared to public via GitHub repository (https://github.com/dxunit-sam/wheres-my-tabby) as part of the project code, with structure for users to add their own data.
- Is it subject to any copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?  
  - Mackenzie photos: Owned by the creator (dxunit-sam); personal use or appreciation only, no explicit license.  
  - Other tabby photos: From Kaggle under Kaggle's terms (likely CC-BY-SA or public domain; check dataset page for specifics).

### Maintenance
- Who maintains the dataset?  
  The creator (dxunit-sam) maintains it personally via the GitHub repository. Updates may include more Mackenzie photos or expanded breeds. Kaggle data is maintained by the Kaggle project owner.