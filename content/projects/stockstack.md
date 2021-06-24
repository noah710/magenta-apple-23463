---
title: StockStack
subtitle: Web Programming class project
date: '2021-05-01'
thumb_img_alt: StockStack Welcome
content_img_alt: StockStack Portfolio
excerpt: >-
  Web based stock and portfolio tracking service
canonical_url: stockstack
layout: post
thumb_img_path: images/SS_Dash.png 
content_img_path: images/SS_Dash.png 
---
## Overview

StockStack (SS) integrates with Yahoo Finance to provide data on trending stocks. SS also allows users to create and track stock portfolios.<br><br>

I deployed this app on GCP AppEngine, check it out [here!](https://cs1520-stockstack.uc.r.appspot.com/). If the tickers don't load in quickly, try refreshing your page. The app scales with the traffic it receives (usually none) so if things aren't loading, chances are the instance is just spinning up! 

[Github](https://github.com/noah710/StockStack)

### Technical Contributions
As the team lead for this project, I worked with each of my team members to orchestrate our full stack web application. My main technical contributions were:
#### Async loading of tickers on homepage
Displaying 40 tickers on the homepage meant making 40 requests from the SS backend to Yahoo Finance. This lead to unacceptablely long load times on the front page (~5 seconds), so I created:
 - An endpoint for the frontend to query for a list of trending tickers
 - An endpoint for the frontend to query for the price of an individual ticker
 - The frontend JS to asyncronously load the prices of each ticker
This eliminated the bottleneck when loading the homepage.
![async_loading](https://user-images.githubusercontent.com/42897161/117897349-9e8ce280-b290-11eb-82b2-1e08ba48beaf.gif)
#### User portfolio backend+database and frontend
I used GCP DataStore with my Flask backend and pure JS/HTML/CSS frontend to create an intuitive portfolio feature.  
##### User portfolio and removing from portfolio
![profile_load_remove](https://user-images.githubusercontent.com/42897161/117897354-a0ef3c80-b290-11eb-8aa9-d601ce030cd7.gif)

#### Adding to user portfolio
![portfolio_add](https://user-images.githubusercontent.com/42897161/117897358-a482c380-b290-11eb-8d99-1f0f33a5baee.gif)