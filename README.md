# SENMETER
 sentimental analysis

analyss the users sentiment based of social media posts

aim is to read texts from twitter and facebook files and use linguistic markers present in them to analyse mood.
the mood analysed over the last 10 posts (or over time, if it is a frequent user) is the current mood.
This shall also measure post interaction, i.e. if a user has been engaging with posts tagged as "sad" more recently the current mood will be hinting towrds sad.

current mood = [0,1,2,3,4] on a 5 point scale...0 being lowest.

based of this the programme will have recommended activities.
the programme will have a default set of recommended activities but it can be modified by th user according to their needs.
the idea is to make it into an appliaction that sends the recommended activities as notifications.

I've used python to analyze tweets, the code in the above folder... 
___________________________________________________________________________________________________________________________________________________________________________________

For the code to work you need to have a twitter.csv folder from where it'll analyse the tweets.
IDE for pyhon, 
