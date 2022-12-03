# Stable Diffusion on CoreML Apple Silicon

https://machinelearning.apple.com/research/stable-diffusion-coreml-apple-silicon
https://towardsdatascience.com/turn-vs-code-into-a-one-stop-shop-for-ml-experiments-49c97c47db27

## Abstract
For simplicity I created a conda env which includes the [apple dependencies](https://github.com/apple/ml-stable-diffusion) for stable diffusion. Following the Setup Process is simpler in this way.



## Setup Process

```bash
conda env create -f environment.yml
pip install -r requirements.txt
huggingface-cli login
```

### DVC Experiment Tracking

```bash
dvc init
```

## Conversion Process

```bash
python -m python_coreml_stable_diffusion.torch2coreml --convert-unet --convert-text-encoder --convert-vae-decoder --convert-safety-checker -o models
```

## Usage

```bash
python -m python_coreml_stable_diffusion.pipeline --prompt "a photo of an astronaut riding a horse on mars" -i models -o data/raw --compute-unit ALL --seed 193
```

![](data/processed/a_photo_of_an_astronaut_riding_a_horse_on_mars/randomSeed_193_computeUnit_ALL_modelVersion_CompVis_stable-diffusion-v1-4.png)

### Misc
```
conda env export > environment.yml
```