---
title: Carnatic Riffusion
---


The guys at <a href="https://www.riffusion.com/" target="_blank">riffusion.com</a> have done some really cool work. They generate music from captions using stable diffusion. The <a href="http://riffusion.com/about" target="_blank">TLDR</a>- get spectogram images for music and train stable diffusion to generate music. 

Using their idea, let's see if we can train something for Carnatic music. 

* First, we collect data for Carnatic music. Youtube will be out data source. There is this really cool <a href="https://ramanarunachalam.github.io/Music/Carnatic/carnatic.html" target="_blank">site</a> which has annotated almost all the songs on Youtube, with raga, tala, composer. I'm picking only instrumental songs for now. 
* Let's pick Sri Lalgudi Jayaram's songs. It takes a little time to work with the JSONs from the repo but definitely doable. We have the youtube links, the raga, tala and composer associated. All we need to do now is to generate spectogram images for the audios and create captions. Captions could be simple, something like this - "Raga Reethigowla and composer Thyagaraja". We can tweak this after first cut results. **You can checkout the dataset <a href="https://docs.google.com/spreadsheets/d/1C5m6KgOA8-IKaWVPknIMQNuZYGaSM-XF/edit?usp=sharing&ouid=112760685178093584686&rtpof=true&sd=true" target="_blank">here</a>**
* Once you have the dataset, all you need to do is run a script from the diffusers library to train. 

* I am sharing some first cut results below. They are not perfect or close to perfect even. We have finished barely an epoch of training and our training data is highly unprocessed.

**Caption: Raga Sindhubhairavi and composer Swathi Thirunal**

<audio controls>
  <source src="./first-cut-results/raga Sindhubhairavi and composer Swathi Thirunal.mp3" type="audio/mpeg">
</audio>

**Caption: Raga Anandabhairavi and composer Shyama Shastri**

<audio controls>
  <source src="./first-cut-results/raga Anandabhairavi and composer Shyama Shastri.mp3" type="audio/mpeg">
</audio>

**Caption: Raga Atana and composer Veena Subbanna**

<audio controls>
  <source src="./first-cut-results/raga Atana and composer Veena Subbanna.mp3" type="audio/mpeg">
</audio>

**Caption: Raga Behag and composer Lalgudi Jayaraman**

<audio controls>
  <source src="./first-cut-results/raga Behag and composer Lalgudi Jayaraman.mp3" type="audio/mpeg">
</audio>

**Caption: Raga Gowla and composer Muthuswami Dikshitar**
<audio controls>
  <source src="./first-cut-results/raga Gowla and composer Muthuswami Dikshitar.mp3" type="audio/mpeg">
</audio>

* Issues:
  * Too much mridangam in the songs - This could be because we have trained on whole songs instead of specific portions of the song. So the Mridangam *tani avartanam* seems to take precedence for many. 
  * The captions are not good. As of now, we generate captions with this template - "Raga {raga name} and composer {composer name}". There is not enough context in this. A better way would be - "Alapanai in raga {raganame} in {talaname} tala", "Neraval in raga {raganame} by {singer name}". Of course, we'd need to segment the songs into *alapanai*, *tani avartanam*, *neraval* and *violin* for this. 
  * The raga is not actually followed in many cases. For this, we could add a loss function with a raga recognition model - or - jointly train a raga detector with SD. 