## 🧠 GREAT: Generalizable Backdoor Attacks in RLHF via Emotion-Aware Trigger Synthesis

🧑‍🔬 **Authors:** Subrat Kishore Dutta, Yuelin Xu, Piyush Pant, Xiao Zhang 


🧬 **AIR-ML Lab**  - [Adversarial, Interpretable, and Robust Machine Learning Lab, CISPA](https://air-ml.org)


📚 **Publication:** [arXiv →](https://arxiv.org/abs/2510.09260)


---

### 🌟 Overview
<div align="center">
  <img src="https://github.com/PiyushWithPant/GREAT/blob/main/assets/overview.jpg" alt="GREAT Overview" width="95%">
</div>


---



### ⚙️ Setup

#### 1️⃣ Create Environment
```bash
conda create -n great python=3.10 -y
conda activate great
pip install -r requirements.txt
```



### 2️⃣ Add Environment Variables

Create a `.env` file in the project root and add:




---

### 🧩 Usage Guide


#### Step 0 - Get the desired Subpopulation

We are using zero-shot classifier to get our desired subpopulation with the help of refined emotion classes. To do it-

```bash
python src/data_processing/subpopulation_selection_using_zs_classifier.py
```

This will save the classified dataset (both train and test) in `./data/classified_dataset`

#### Step 1 — Trigger Embeddings

Compute and cluster emotion-aware triggers:

```bash
python src/clustering/cluster_embeddings.py
```

This will:

- Extract embeddings using a selected LLM (e.g., Llama-3, Gemma, OPT)

- Apply PCA & K-Means clustering

- Save cluster visualizations and medoids

> PS: You will require the Trigger dataset for this step

#### Step 2 — Data Poisoning

Use the generated medoid triggers to create poisoned datasets:

```bash
python src/data_processing/main.py
```

This python file:

- Uses all other helper modules

- Loads clean preference datasets

- Injects emotion-aware triggers into chosen samples

- Saves poisoned datasets for RLHF training

#### Step 3 — RLHF Training Pipeline

Train your SFT and DPO models sequentially:

```bash
python src/pipeline/1_rlhf_training.py
```

Includes:

✅ Supervised Fine-Tuning (SFT)

✅ Parameter-Efficient Fine-Tuning (PEFT)

✅ Direct Preference Optimization (DPO)

#### Step 4 — Response Generation

Generate responses from the trained (potentially poisoned) models:

```bash
python src/pipeline/2_gen_responses.py
```

This step will:

- Use the trained SFT/DPO model

- Generate responses for ASR, ASR_GEN, ASR_GEN_OOD, and UHR datasets

- Save the generated outputs in evaluation/<MODEL_NAME>/model_responses/

#### Step 5 — Evaluation

Evaluate model safety, alignment, and ASR (Attack Success Rate):

```bash
python src/pipeline/3_eval_gpt.py
```

This step will:

- Run GPT-based evaluation for HARMFUL vs HARMLESS responses

- Compute statistics and save JSON evaluation files

- Support multiple seeds for robust analysis

### 📊 Outputs

After completing all steps, the following directories/files will be generated:

- 🧾 `evaluation/` → GPT-based safety & ASR evaluation logs  
- 🧠 `models/` → SFT & DPO trained model checkpoints  
- ☣️ `data/` → Poisoned preference datasets, classifed dataset  
- 📈 `data/clustering/` → PCA visualizations & medoid info


### 📘 Citation

If you find this work useful, please cite:

```bibtex
@misc{dutta2025greatgeneralizablebackdoorattacks,
      title={GREAT: Generalizable Backdoor Attacks in RLHF via Emotion-Aware Trigger Synthesis}, 
      author={Subrat Kishore Dutta and Yuelin Xu and Piyush Pant and Xiao Zhang},
      year={2025},
      eprint={2510.09260},
      archivePrefix={arXiv},
      primaryClass={cs.CR},
      url={https://arxiv.org/abs/2510.09260}, 
}

```


### 🪪 License

This project is released under the **MIT License** — see the [LICENSE](https://github.com/PiyushWithPant/GREAT/blob/main/LICENSE.md) file for details.


### ❤️ Acknowledgments

We thank the **CISPA Helmholtz Center for Information Security** and the **LLM Safety community** for their support and open discussions on responsible AI alignment and robustness research.


# GREAT-Generalizable-Backdoor-Attacks-in-RLHF-via-Emotion-Aware-Trigger-Synthesis
# GREAT-Generalizable-Backdoor-Attacks-in-RLHF-via-Emotion-Aware-Trigger-Synthesis
