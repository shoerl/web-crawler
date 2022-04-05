# CS3700 Project 5: Web Crawler
Group Members: Sean Hoerl & Jess Van de Ven

## High-Level Approach
At a high level, our crawler logs in to fakebook, and then begins crawling until we have seen all 5 secret flags. For crawling, we start at the home page of fakebook, and grab all available links there and then add them to our queue. For each link in our queue, we visit the corresponding page, check to see if a secret flag is present, grab all unseen links present on the page and add them to our queue. We do this until we have gathered all 5 secret flags.



## Challenges

## Properties/Features

## Testing