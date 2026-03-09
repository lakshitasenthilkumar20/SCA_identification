# Fine-Grained Agricultural Monitoring: Distinguishing Sugarcane Aphids from Beneficial Insects through Multilevel Expert Heads

Fine-Grained Agricultural Monitoring

Distinguishing Sugarcane Aphids from Beneficial Insects using Hierarchical Deep Learning

Overview

Accurate identification of agricultural pests is essential for sustainable crop protection. In sugarcane ecosystems, Sugarcane Aphids (SCA) are destructive pests that can cause significant yield losses. However, distinguishing them from beneficial insects such as predator ladybugs is challenging due to visual similarity and extreme class imbalance.

This project proposes a hierarchical deep learning framework with multiple expert classification heads designed to mirror the biological taxonomy of insects. The model addresses the “majority drowning” problem, where abundant non-pest samples overwhelm the learning signal of rare pest classes.

The framework improves minority class detection, particularly for Sugarcane Aphids, while maintaining high performance across the entire insect taxonomy.

⸻

Key Features
	•	Hierarchical multi-level classification architecture
	•	Specialized expert heads aligned with insect taxonomy
	•	Shared CNN backbone for efficient feature extraction
	•	Class-balanced adaptive focal loss to handle severe class imbalance
	•	Hierarchical coherence loss to enforce taxonomic consistency
	•	Improved detection of rare pest species

⸻

Problem Statement

Agricultural pest detection datasets often exhibit extreme class imbalance. In this dataset:
	•	Sugarcane Aphid samples represent only ~3% of the data
	•	Most samples belong to non-pest insects and beneficial predators

Traditional flat classifiers treat all classes equally, causing the model to prioritize majority classes while ignoring rare pests.

This project addresses the problem by introducing a taxonomy-aware hierarchical classification system.

⸻

Dataset

Images were collected from multiple sources:
	•	Training data: iNaturalist
	•	Testing data: Google Images and Bing Images (to evaluate domain shift)

The dataset contains:

Predator Ladybugs
	•	Cycloneda sanguinea
	•	Olla v-nigrum
	•	Coleomegilla maculata
	•	Scymninae
	•	Hippodamia convergens
	•	Harmonia axyridis
	•	Coccinella septempunctata
	•	Adalia bipunctata
	•	Adalia decempunctata
	•	Calvia quattuor-guttata
	•	Diomus terminatus
	•	Scymnus loewii
	•	Hippodamia tredecimpunctata

Other Predators
	•	Green lacewing
	•	Hoverflies
	•	Minute pirate bugs

Non-Predatory Ladybugs
	•	Epilachna varivestis
	•	Psyllobora vigintiduopunctata
	•	Henosepilachna vigintipunctata

Other Agricultural Insects
	•	Leafhoppers
	•	Planthoppers
	•	Mealybugs
	•	Chrysomelidae
	•	Curculionidae
	•	Aleyrodidae
	•	Thysanoptera
	•	Pentatomidae
	•	Crambidae
	•	Noctuidae

Target Pest
	•	Sugarcane Aphid (SCA)

⸻

Data Preprocessing

The images were captured under real-world field conditions, introducing challenges such as:
	•	cluttered backgrounds
	•	illumination changes
	•	varying insect scales
	•	occlusions

To address this, the preprocessing pipeline includes:
	•	image resizing and normalization
	•	duplicate removal
	•	stratified train–validation split
	•	geometric augmentation
	•	horizontal flipping
	•	small-angle rotations
	•	photometric augmentation
	•	brightness changes
	•	contrast adjustments
	•	color jitter

⸻

Hierarchical Classification Architecture

The proposed model consists of three main components:

1. Shared Backbone

A convolutional neural network extracts general visual features from insect images.

Benefits:
	•	reduces model complexity
	•	enables feature sharing across hierarchy levels

⸻

2. Multi-Level Expert Heads

Separate classification heads operate at different levels of the hierarchy:

Level 1
→ SCA vs Non-SCA

Level 2
→ Predator vs Non-Predator

Level 3
→ Species-Level Classification

Each head specializes in a different level of semantic granularity.

⸻

3. Loss Functions

Adaptive Class-Balanced Focal Loss

Addresses extreme imbalance by reducing the dominance of majority classes.

Branch-Aware Cross Entropy

Balances gradients across hierarchical branches with different class counts.

Hierarchical Coherence Loss

Ensures logical consistency in predictions by enforcing:

P(child) ≤ P(parent)


⸻

Training Strategy

Training is performed in two stages:

Stage 1
	•	Backbone frozen
	•	Train only the root classifier
	•	Stabilizes minority class detection

Stage 2
	•	All parameters trained jointly
	•	Full loss function applied

⸻

Workflow
	1.	Dataset collection
	2.	Duplicate removal
	3.	Image preprocessing
	4.	Data augmentation
	5.	Class imbalance handling
	6.	Model training
	7.	Cross-source testing

⸻

Results

Effect of Data Augmentation

Model	Accuracy	Macro F1
Flat (Original)	0.8187	0.7723
Flat (Augmented)	0.8070	0.7707

Data augmentation improved minority class learning despite slightly lower overall accuracy.

⸻

Flat vs Hierarchical Model

Model	Accuracy	Macro F1
Flat Baseline	0.8070	0.7707
Hierarchical Model	0.8666	0.8376

Hierarchical classification significantly improves overall performance.

⸻

Sugarcane Aphid Detection

Model	Precision	Recall	F1
Flat Model	0.537	0.7838	0.6374
Hierarchical Model	0.775	0.8378	0.8052

The hierarchical model dramatically improves detection of the rare SCA pest.

⸻

Future Work

Future improvements may include:
	•	cross-season insect datasets
	•	part-based insect localization
	•	insect-aware segmentation
	•	integration of contextual information such as:
	•	crop type
	•	geographical location
	•	seasonal data

⸻

Applications
	•	Precision agriculture
	•	Automated pest monitoring
	•	Integrated pest management
	•	Smart farming systems
	•	Real-time field pest detection

⸻

Tech Stack
	•	Python
	•	PyTorch
	•	Deep Learning
	•	Computer Vision
	•	Hierarchical Classification

⸻

Authors

Lakshita S
Madhura Bashini M S
Dr. Kirubavathi

⸻

License

This project is intended for research and academic purposes.
