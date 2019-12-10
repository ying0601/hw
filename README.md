#擷取 Avengers Endgame (2019) 的上映日期列表
import requests
movie_url = "https://www.imdb.com/title/tt4154796/releaseinfo?ref_=tt_dt_dt#releases"
response = requests.get(movie_url)
response_text = response.text
!pip install -U beautifulsoup4
from bs4 import BeautifulSoup
soup = BeautifulSoup(response_text)  
movie_release_date_cs =".release-date-item__date"
movie_release_date = [elem.text.strip() for elem in soup.select(movie_release_date_cs)]
print(movie_release_date)
movie_release_country_cs =".release-date-item__country-name"
movie_release_country=[elem.text.strip() for elem in soup.select(movie_release_country_cs)]
print(movie_release_country)
import pandas as pd
upper_df = pd.DataFrame()
lower_df = pd.DataFrame()
upper_df['country'] = movie_release_country
lower_df['date'] = movie_release_date
movie_release_df = pd.concat([upper_df, lower_df],axis=1)
movie_release_df['date'].mode()
movie_release_df[movie_release_df["date"]=='24 April 2019']["country"]
len(movie_release_df[movie_release_df["date"]=='24 April 2019']["country"])
