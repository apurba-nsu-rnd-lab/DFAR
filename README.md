# Beyond Labels: Aligning Large Language Models with Human-like Reasoning
This is the repository for "Beyond Labels: Aligning Large Language Models with Human-like Reasoning" by Muhammad Rafsan Kabir, Rafeed Mohammad Sultan, Ihsanul Haque Asif, Jawad Ibn Ahad, Fuad Rahman, Mohammad Ruhul Amin, Nabeel Mohammed, and Shafin Rahman, accepted to be presented at ICPR 2024.

## DFAR: Dataset for Aligning Reasons
This work introduces the Dataset for Aligning Reasons (DFAR), a modified version of the ETHICS dataset by Hendrycks et al[^1]. DFAR consists of ethical statements, their corresponding labels, and reasons explaining the ethical judgments.

[The DFAR dataset is available here](<https://github.com/apurba-nsu-rnd-lab/DFAR/tree/main/DFAR%20dataset>)

**Train-test split**: The DFAR dataset is divided into two subsets: a training set and a test set, with a split ratio of 90% to 10%. Consequently, the training set consists of 4,500 data points, while the test set comprises 500 data points.

***NOTE***: *Label consists of two distinct values: 0 and 1, where 0 represents ethical and 1 represents unethical.*

### DFAR Dataset Statistics and Demographic Profile of Dataset Annotators

<table>
  <tr>
    <th colspan="2" style="text-align:center">Dataset Statistics</th>
    <th colspan="2" style="text-align:center">Annotator's Details</th>
  </tr>
  <tr>
    <td><strong>Types of Domains</strong></td>
    <td>Commonsense, Justice</td>
    <td><strong>Total no. of annotators</strong></td>
    <td>12</td>
  </tr>
  <tr>
    <td><strong>Min. Text Length</strong></td>
    <td>151</td>
    <td><strong>No. of female annotators</strong></td>
    <td>6</td>
  </tr>
  <tr>
    <td><strong>Max. Text Length</strong></td>
    <td>1171</td>
    <td><strong>No. of male annotators</strong></td>
    <td>6</td>
  </tr>
  <tr>
    <td><strong>Avg. Text Length</strong></td>
    <td>467.45</td>
    <td><strong>Avg. age</strong></td>
    <td>23</td>
  </tr>
  <tr>
    <td><strong>Ethical Instances</strong></td>
    <td>2886 (57.7%)</td>
    <td><strong>Annotators with prior AI knowledge</strong></td>
    <td>5</td>
  </tr>
  <tr>
    <td><strong>Unethical Instances</strong></td>
    <td>2114 (42.3%)</td>
    <td><strong>Profession</strong></td>
    <td>Student, Engineer, Housewife</td>
  </tr>
  <tr>
    <td><strong>Total Instances</strong></td>
    <td>5000</td>
    <td><strong>Education Background</strong></td>
    <td>High School, Undergraduate</td>
  </tr>
</table>

<br> 

## Methodology


**Figure**: (a) Fine-tuning using labels only and (b) Fine-tuning using both labels & reasons on the DFAR dataset. The first approach involves training the model on the ethical-unethical labels without incorporating the accompanying reasons. LLM L produces $\hat{y_i}$ based on the input $x_i$ that passes through the embedding layer. LLM's weights are being updated based on the loss. In our novel approach, LLM (L) generates $\hat{y_i}$ and $\hat{r_i}$ based on the input $x_i$. LLM is fine-tuned based on the loss ($\mathcal{L}$) between embeddings of $\hat{y_i}$, $\hat{r_i}$, and $y_i$, $r_i$ of the dataset.
![Screenshot from 2024-08-17 22-58-50](https://github.com/user-attachments/assets/e6977713-3a4f-4c6d-b391-56800725c469)


<br> 

## Results

<h2>Comparison of Evaluation Results on DFAR and ETHOS</h2>

<p><strong>Note</strong>: ↑ (higher is better), ↓ (lower is better). `-` denotes results that are not applicable.</p>

<table>
  <thead>
    <tr>
      <th>Method</th>
      <th>Models</th>
      <th>DFAR MAR (%) ↓</th>
      <th>DFAR Acc. (%) ↑</th>
      <th>ETHOS MAR (%) ↓</th>
      <th>ETHOS Acc. (%) ↑</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="6"><strong>Non-Generative Methods</strong></td>
      <td>SVM</td>
      <td>-</td>
      <td>69.4</td>
      <td>-</td>
      <td>66.4</td>
    </tr>
    <tr>
      <td>Random Forests</td>
      <td>-</td>
      <td>78.6</td>
      <td>-</td>
      <td>65.0</td>
    </tr>
    <tr>
      <td>Gradient Boosting</td>
      <td>-</td>
      <td>63.2</td>
      <td>-</td>
      <td>64.3</td>
    </tr>
    <tr>
      <td>Logistic Regression</td>
      <td>-</td>
      <td>67.8</td>
      <td>-</td>
      <td>66.9</td>
    </tr>
    <tr>
      <td>BERT</td>
      <td>-</td>
      <td>78.6</td>
      <td>-</td>
      <td>79.9</td>
    </tr>
    <tr>
      <td>DistilBERT</td>
      <td>-</td>
      <td>78.2</td>
      <td>-</td>
      <td><strong>80.4</strong></td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Generative Models</strong></td>
      <td>Mistral 7B <br>(Pre-trained)</td>
      <td>35.4</td>
      <td>45.4</td>
      <td>9.6</td>
      <td>54.7</td>
    </tr>
    <tr>
      <td>Mistral 7B <br>(Fine-tuned L)</td>
      <td>18.6</td>
      <td>47.4</td>
      <td>10.6</td>
      <td>56.8</td>
    </tr>
    <tr>
      <td>Mistral 7B <br>(Ours L+R)</td>
      <td>12.2</td>
      <td>82.2</td>
      <td><strong>5.3</strong></td>
      <td>59.6</td>
    </tr>
    <tr>
      <td>Llama-2 7B <br>(Pre-trained)</td>
      <td>52.0</td>
      <td>36.4</td>
      <td>32.8</td>
      <td>12.0</td>
    </tr>
    <tr>
      <td>Llama-2 7B <br>(Fine-tuned L)</td>
      <td>38.4</td>
      <td>62.8</td>
      <td>33.7</td>
      <td>54.1</td>
    </tr>
    <tr>
      <td>Llama-2 7B <br>(Ours L+R)</td>
      <td><strong>9.4</strong></td>
      <td><strong>89.4</strong></td>
      <td>18.6</td>
      <td>78.8</td>
    </tr>
  </tbody>
</table>

<h3>Notes</h3>
<ol>
  <li>The <strong>non-generative models</strong> were fine-tuned on both DFAR and ETHOS datasets and evaluated within these datasets.</li>
  <li>The <strong>generative models</strong> were fine-tuned solely on the DFAR dataset and evaluated within the dataset (DFAR) as well as on cross-dataset (ETHOS). They could not be fine-tuned on ETHOS due to the absence of reasoning in the dataset.</li>
</ol>

<br>

## Installation

```python
pip install torch -qU
pip install transformers -qU
pip install trl -qU
pip install accelerate -qU
pip install bitsandbytes -qU
pip install peft -qU
pip install datasets -qU
```
<br>

## References
[^1]: Hendrycks, D., Burns, C., Basart, S., Critch, A.C., Li, J.L., Song, D., Steinhardt, J.: Aligning ai with shared human values. In: International Conference on Learning Representations (2021) [URL](https://openreview.net/forum?id=dNy_RKzJacY)
