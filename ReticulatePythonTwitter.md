ReticulatePythonTwitter
================
Ingrid Baade
April 1, 2018

I'm going to try to use Reticulate to facilitate using Python in R Markdown. I will create a histogram of tweet hashtags from a sample collected on the 1st of April which was April Fool's Day/ Easter Sunday this year. The first assignment of the Data Science at Scale Course was to get samples of Tweets. There are a number of ways to do this. I haven't include the code for getting the tweets because it has API keys in it, but the resulting text files of tweets are read by the python script in the python chunks of this R Markdown document and hash tags extracted. The top twenty hash tags are returned. I put the tweets in a number of files because I was worried about file size. The returned files of the top 20 hashtags have non-ascii characters. I was running python on windows and even though it was uninterpretable in the Windows console window, the assignment grader accepted the non-ascii characters (after putting some .encode utf-8 stuff in my assignment). Looking at the top 20 hashtags in the notepad++ editor, I can at least see characters from different languages rather than ascii psychobabble smoosh.

Update: Running code chunks produces beautiful markdown with Thai, Korean and Japanese characters. I'm using python 2.7 rather than 3 as you can see from the print statements (python 2) rather than print functions (python 3).

Running the code chunks with python 3 print functions; I can't get the chacters to output, just encodings. There must be a reason the Data At Scale course uses python 2 so I'll stick with python 2.

However, I can't get knit to work with python 2. I'm going to comment out the print statements and try again to knit. I have found out that you can't pass variables in and out of python/r chunks when running chunks, but you can when you knit.

``` r
#install.packages("reticulate")
#library(reticulate)
```

Python assignment: extracts hashtags and stores them as keys with value = count. Returns the top 20 hashtags.

I ran this first at about midday Easter Sunday, Australian east coast time. This is about 3am GMT.

``` python
import json
import sys
import codecs
#def hw():
#  print 'Hello, world!' 
#def lines(fp):
#  print str(len(fp.readlines()))
def main():
  #hw()
  #tweetfile = codecs.open("output2.txt", 'rU', 'utf-8')
  #lines(tweetfile)
  #tweetfile.close()
  
  hashtag_dict={}
  try:
    tweetfiles = [codecs.open("output%d.txt" % i, "rU", "utf-8") for i in range(2, 8)]
    for tweetfile in tweetfiles:
      for line in tweetfile:
        jsondict = json.loads(line)
        if 'entities' in jsondict:
          if 'hashtags' in  jsondict['entities']:
            tweet_tags = jsondict['entities']['hashtags']     
            for i in range(len(tweet_tags)):
              htag = tweet_tags[i]['text'].encode("utf-8")      
              if htag not in hashtag_dict:
                hashtag_dict[htag] = 1
              else:
                hashtag_dict[htag] = hashtag_dict[htag] + 1
  finally:
    for tweetfile in tweetfiles:
      tweetfile.close()
  #for k, v in sorted(hashtag_dict.items(), key=lambda x: x[1], reverse = True)[:20]:
  #  print k, v
  
if __name__ == '__main__':
  main()
```

The top tweet is (Google) translated as "Tilly". It seems though, to be an abbreviated version of the 14th one which translates as "Make a fortune", which is a nice sentiment but I'm not sure if it relates to Easter, April Fool's day or something else! Google thinks these are Thai.

The second hashtag is Japanese and translates to "April Fools".

The sixth, eight and tenth hashtags are Korean for "Ten", "Warner One" and "Amit". Other Korean hashtags are the seventeenth: "Come on. \_Amy Night is the first time.", nineteenth: "Exo", and twentieth: "Fresh seven". (A big k-pop festival is happenning atm I just found out.)

This just leaves number 12 requiring translation. It is Japanese and might mean "2018 \_ Your erotic rank".

NTRs BirthdayIn50Days refers to an Indian movie star. TEN, NCT, BT21, GOT7, EXO and BTS are Korean pop culture references. BBB18 is Big Brother Brazil.

"Hello\_We \_Are\_Beardtan" has not been able to beat "NTRsBirthdayIn50Days" as a popular tweet hashtag in the sample I have collected.

``` python
import json
import sys
import codecs
hashtag_dict={}
try:
  tweetfiles = [codecs.open("output%d.txt" % i, "rU", "utf-8") for i in range(8, 12)]
  for tweetfile in tweetfiles:
    for line in tweetfile:
      jsondict = json.loads(line)
      if 'entities' in jsondict:
        if 'hashtags' in  jsondict['entities']:
          tweet_tags = jsondict['entities']['hashtags']   
          for i in range(len(tweet_tags)):
            htag = tweet_tags[i]['text'].encode("utf-8")        
            if htag not in hashtag_dict:
              hashtag_dict[htag] = 1
            else:
              hashtag_dict[htag] = hashtag_dict[htag] + 1
finally:
  for tweetfile in tweetfiles:
    tweetfile.close()
    
# To see the Korean, Japanese and Thai characters, run this chunk using python 2.   
#for k, v in sorted(hashtag_dict.items(), key=lambda x: x[1], reverse = True)[:20]:
#  print k, v
  
```

This one was run at 11.00pm Australian east coast time (approx 2pm GMT).

The Thai language "Tilly" has dropped to 6th spot.

Korean:The second one translates to "Warner One". The eight one is "Fresh seven".The tenth one is "I love you guys." The seventeenth: "Let's walk together\_JBJ", eighteenth: "Kang Daniel" and twentieth "twice".

The 7th, 11th and 15th ones are Japanese, respectively "Something", "The 2nd anniversary of AVEMA TV" and "April Fool".

JIMIN, BTS, WINNER0404COMEBACK, Eyesonyou, Wannaone, Twice, Look are Korean pop culture references.

GATPAT is a test for school children in Thailand. (I think).

MasterChefThailand is the most hashtagged hashtag in the sample I have collected tonight.

``` r
# doesn't work
```
