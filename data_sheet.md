## Datasheet for Where's My Tabby?

### Motivation
- For what purpose was the dataset created?  
  The dataset was created to train and test an AI model for identifying an individual tabby cat (Mackenzie) from other tabby cats, as a proof-of-concept for lost pet recognition using photos. This serves as the capstone project for the Professional Certificate in Machine Learning and Artificial Intelligence at Imperial College.

- Who created the dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)? Who funded the creation of the dataset?  
  Created by dxunit-sam (the project owner) as part of their individual capstone project at Imperial College. No external funding; self-funded through personal resources and course participation.

### Composition

- What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?  
  The dataset consists of RGB photos of cats: one class for Mackenzie (the owner's cat) and another for other tabby cats.

- How many instances of each type are there?  
  - Mackenzie: ~100+ photos (so far)
  - Other tabby cats: ~500 photos (sampled from larger set).  
  Total: ~600+ photos.

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