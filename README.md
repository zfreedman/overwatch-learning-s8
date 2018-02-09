# MLND Capstone

This project uses supervised learning in an attempt to classify competitive Overwatch players based by SR.

## Getting Started

### Conda Requirements

The conda environment requirements are in ./requirements.txt.

### File Structure

#### ./data/
 
 This directory contains all hero data. Previously scraped data exists here, and newly scraped data will be output to here. ./data/hero_processed/ and ./data/raw/ are 2 different datasets.

 The ./data/post_scrape_cleanup/ directory contains the contents of the above mentioned directories in cleaned format, where duplicates and dirty entries are removed.

 The files in both these directories are in CSV format.

 Additionally, this directory contains indexers for 2 different jupyter notebooks described later in ./scrape/

#### ./learning/

This directory contains the machine learning notebook. In the current state of this code as of 2/6/2018 at 5:37am PST, after conda requirements are installed (there may be a pip requirement or 2 that will throw an error), the learning notebook should be ready to run as is without scraping additional data.

#### ./post_scrape_cleanup/

This directory houses the code that's responsible for cleaning the ./data/hero_processed/ and ./data/raw/ directory CSVs and writing the cleaned contents to ./data/post_scrape_cleanup/.

#### ./scrape/

discovery_scrape

This jupyter noteboook is responsible for scraping battletags on the OverwatchTracker competitive leaderboard. The scraped battletags are written to ../data/discovery.csv. Additionally, the current page index for scraping is maintained in ../data/discovery_curr_page.txt.

discovery_scrambler

This jupyter notebook literally just scrambles the battletags scraped from discovery_scrape. It's meant to only be run once, or after a set of battletags has been added. This does not have to be run unless new data needs to be collected. In this case, the old battletags should probably be removed. discovery_scrape does not take long (< 1 hour on a desktop)

OverwatchTracker lists battletags on the competitive leaderboard in order of SR. Therefore, the battletags are scraped from Grandmaster to Bronze. However, hero_scrape scrapes the actual performance data for each battletag's played hero, which takes significantly longer (days or even weeks). Because of this, machine learning can be started with an incomplete dataset so long as some type of SR distribution is collected. If the battletags weren't scrambled, you'd get every Grandmaster player before getting any other SR class.

The scrambled battletags are output to ../data/discovery_scrambled.csv.

hero_scrape

This juypter notebook is responsible for scraping PlayOverwatch competitive hero data for each battletag scraped from discovery_scrape. The scraped data is periodically written to ../data/hero_processed/ and ../data/raw/. It can be run as is, but more data is not necessarily needed at this time. The dataset has currently observed over 90K entries out of 160K+.

The index of the last scraped battletag from the scrambled battletags file, ../data/discovery_scrambled.csv, is in ../data/curr_battletag_index_from_scrambled.txt.

### Machine Learning

In order to see the results of the machine learning, after installing the conda requirements, type "jupyter notebook" into your terminal or command prompt from the same directory this README is in. The machine learning notebook is in ./learning/. Open the learning.ipynb and run all cells.

## Authors

Zach Freedman