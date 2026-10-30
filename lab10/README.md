# Lab 10 – English→French Seq2Seq: 20,000 vs 80,000 sentence pairs
 
Both notebooks use the **same model and settings**; the only change is `N_SAMPLES` (20,000 → 80,000).
  
## Results
 
| | 20,000 pairs | 80,000 pairs |
|---|---|---|
| English vocab | 5,699 | 9,516 |
| French vocab | 9,779 | 18,900 |
| Model parameters | 5.28 M | 9.28 M |
| Final train accuracy | 59.3% | 86.5% |
| Final validation accuracy | 50.2% | 67.5% |
| Final validation loss | 3.31 | 2.01 |
| **Test accuracy** | **50.6%** | **67.4%** |
| **Test loss** | **3.25** | **2.00** |
| Training time per epoch | about 50 s | about 170 s (first epoch 306 s) |
 
## Sample translations
 
| English | 20k model | 80k model |
|---|---|---|
| Hello | *(empty)* | j'ai été frappé . |
| How are you? | qu'est-ce qui sont ? | comment allez-vous ? ✅ |
| I love you | je suis ici ? | j'adore vous ? (close) |
| Thank you | où vous plaît ? | tu vas fais ? |
| I am hungry | je suis détendue . | j'ai faim ! ✅ |
| Where are you? | où es-tu ? ✅ | où vous êtes ? ✅ |
 
## Observations
 
1. **More data clearly helps.** Test accuracy rises by about 17 points (50.6% → 67.4%) and test loss drops from 3.25 to 2.00. The 80k model gets 3 of 6 sample sentences right; the 20k model gets 1.
2. **The 20k model had too little data.** Its train and validation curves were still improving at epoch 20, but its translations were mostly wrong and "Hello" came out empty. That is probably because the word was missing from the sample and was dropped by the tokenizer.
3. **The 80k model starts to overfit.** Train accuracy keeps climbing (86.5%) while validation accuracy flattens around 67%, and validation loss bottoms out at epoch 17 (1.99) then rises slightly. About 15–17 epochs would be enough; adding dropout or early stopping would help.
4. **Rare phrases are still weak.** "Hello" and "Thank you" are very short, uncommon in a dataset made of longer sentences, and still translate wrongly in the 80k model. The dataset favors full sentences over greetings.

## Conclusion
 
Quadrupling the training data gave a large, clear improvement at the same architecture, which shows that data size was the main bottleneck. Further gains would likely need more data or epochs with early stopping, attention, beam search, or a pretrained Transformer model (e.g. MarianMT).
 
*Note: accuracy here is per-word accuracy under teacher forcing, so it overstates real translation quality. BLEU on the held-out test split would be a fairer comparison.*
 
