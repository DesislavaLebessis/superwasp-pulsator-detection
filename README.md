[README.md](https://github.com/user-attachments/files/25825869/README.md)
# SuperWASP Pulsator Detection

Automated classification of pulsating variable stars in SuperWASP light curves using deep learning (ResNet18 + Transfer Learning).

## Results

| Phase | F1-Score | Accuracy |
|-------|----------|----------|
| Phase 1 — classifier only | 0.694 | 69.9% |
| Phase 2 — fine-tuning | **0.802** | **80.2%** |

## Dataset

**Zenodo VeSPA** — SuperWASP variable star classifications  
McMaster et al. 2021, Res. Notes AAS 5 228  
DOI: [10.5281/zenodo.14937227](https://doi.org/10.5281/zenodo.14937227)  
License: Creative Commons Attribution 4.0

| Class | Images |
|-------|--------|
| Pulsators | 1,999 |
| Non-pulsators | 2,000 |
| **Total** | **3,999** |

## Method

- **Architecture:** ResNet18 pre-trained on ImageNet
- **Phase 1:** Only the classifier head is trained (frozen backbone)
- **Phase 2:** Fine-tuning of layer3 + layer4 + classifier with lower learning rate (5e-5)
- **Augmentation:** Random crop, horizontal/vertical flip, rotation, color jitter
- **Early stopping:** patience = 8 epochs

## How to Use

### Requirements

```bash
pip install -r requirements.txt
```

### Step 1 — Download data

Open `superwasp_01_download.ipynb` in Google Colab and run all cells.  
This downloads ~4,000 light curve images from Zenodo to your Google Drive.

### Step 2 — Train model

Open `superwasp_02_training.ipynb` in Google Colab.  
Enable GPU: **Runtime → Change runtime type → GPU (T4)**  
Run all cells. The trained model is saved to your Google Drive.

### Adjust paths

In both notebooks, update this line to match your Google Drive folder:

```python
BASIS_PFAD = '/content/drive/MyDrive/SuperWASP'
```

## Repository Structure

```
superwasp-pulsator-detection/
    superwasp_01_download.ipynb   ← Download images from Zenodo
    superwasp_02_training.ipynb   ← Train ResNet18 model
    requirements.txt              ← Python dependencies
    README.md
```

## Citation

If you use this code or dataset, please cite:

```
McMaster et al. 2021, Res. Notes AAS 5 228
DOI: 10.5281/zenodo.14937227
```

## Author

**Desislava Lebessis**  
Citizen Scientist — SuperWASP / Zooniverse  
[GitHub](https://github.com/YOUR-USERNAME) · www.linkedin.com/in/desislava-lebessis-57aa77b4

## License

MIT License — see [LICENSE](LICENSE) for details.
