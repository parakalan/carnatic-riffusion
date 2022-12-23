---
title: Carnatic Riffusion
---


The guys at <a href="https://www.riffusion.com/" target="_blank">riffusion.com</a> have done some really cool work. They generate music from captions using stable diffusion. The <a href="http://riffusion.com/about" target="_blank">TLDR</a>- get spectogram images for music and train stable diffusion to generate music. 

Using their idea, let's see if we can train something for Carnatic music. 

* First, we collect data for Carnatic music. Youtube will be out data source. There is this really cool <a href="https://ramanarunachalam.github.io/Music/Carnatic/carnatic.html" target="_blank">site</a> which has annotated almost all the songs on Youtube, with raga, tala, composer. I'm picking only instrumental songs for now. 
* Let's pick Sri Lalgudi Jayaram's songs. It takes a little time to work with the JSONs from the repo but definitely doable. We have the youtube links, the raga, tala and composer associated. All we need to do now is to generate spectogram images for the audios and create captions. Captions could be simple, something like this - "Raga Reethigowla and composer Thyagaraja". We can tweak this after first cut results. **You can checkout the dataset <a href="https://docs.google.com/spreadsheets/d/1C5m6KgOA8-IKaWVPknIMQNuZYGaSM-XF/edit?usp=sharing&ouid=112760685178093584686&rtpof=true&sd=true" target="_blank">here</a>**
* Once you have the dataset, all you need to do is run a script from the diffusers library to train. 

* I am sharing the first cut results below. These are not handpicked and might not sound good, but note that this is after training just over an epoch. 

<audio controls>
  <source src="horse.mp3" type="audio/mpeg">
</audio>