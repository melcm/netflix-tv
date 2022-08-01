# netflix-tv
python code
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import seaborn as sns
import matplotlib.pyplot as plt

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
netflix=pd.read_csv('/kaggle/input/netflix-shows/netflix_titles.csv')
netflix.head()
netflix.info()
netflix.shape
netflix.isnull().sum()
netflix.nunique()
#Type : Movies or Tv Show
sns.countplot(netflix['type'],color='grey',orient='v')
plt.tight_layout()
netflix['type'].value_counts()
pd.crosstab(netflix.release_year, netflix.type).plot(kind='bar',figsize=(15,15))
Release Year
#tahun realease
def release(release_date):
    if 1960<=release_date<=1990:
        return 'Very old'
    elif 1990<release_date<= 2000:
        return 'Old'
    elif 2000<release_date<=2015:
        return 'Early 21st century'
    elif 2015<release_date<=2021:
        return 'New'
    else:
        return None
netflix['Movie Release type']=netflix['release_year'].apply(release)
netflix
t=netflix.groupby('Movie Release type').type.value_counts()
t
#plt.figure(figsize=(13,8))
sns.countplot(netflix['Movie Release type'][:],hue=netflix['type'],color='grey')
netflix[netflix['type']=='TV Show'].sort_values('release_year').tail(15)
netflix[netflix['type']=='Movie'].sort_values('release_year').tail(15)
netflix.groupby('rating').type.value_counts()
plt.figure(figsize=(13,8))
sns.countplot(netflix['rating'][:],hue=netflix['type'],color='Purple')
x= netflix['country'].value_counts().head(20)
x
sns.barplot(x=x.values,y=x.index)
print('10 Negara Top Movie')
netflix.groupby('type').country.value_counts()['Movie'][:10]
print('10 Top TV Show')
netflix.groupby('type').country.value_counts()['TV Show'][:10]
n= netflix['listed_in'].value_counts()[:20]
n
sns.barplot(x=n.values,y=n.index)
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import seaborn as sns
import matplotlib.pyplot as plt

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
/kaggle/input/netflix-shows/netflix_titles.csv
netflix=pd.read_csv('/kaggle/input/netflix-shows/netflix_titles.csv')
netflix.head()
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description
0	s1	TV Show	3%	NaN	João Miguel, Bianca Comparato, Michel Gomes, R...	Brazil	August 14, 2020	2020	TV-MA	4 Seasons	International TV Shows, TV Dramas, TV Sci-Fi &...	In a future where the elite inhabit an island ...
1	s2	Movie	7:19	Jorge Michel Grau	Demián Bichir, Héctor Bonilla, Oscar Serrano, ...	Mexico	December 23, 2016	2016	TV-MA	93 min	Dramas, International Movies	After a devastating earthquake hits Mexico Cit...
2	s3	Movie	23:59	Gilbert Chan	Tedd Chan, Stella Chung, Henley Hii, Lawrence ...	Singapore	December 20, 2018	2011	R	78 min	Horror Movies, International Movies	When an army recruit is found dead, his fellow...
3	s4	Movie	9	Shane Acker	Elijah Wood, John C. Reilly, Jennifer Connelly...	United States	November 16, 2017	2009	PG-13	80 min	Action & Adventure, Independent Movies, Sci-Fi...	In a postapocalyptic world, rag-doll robots hi...
4	s5	Movie	21	Robert Luketic	Jim Sturgess, Kevin Spacey, Kate Bosworth, Aar...	United States	January 1, 2020	2008	PG-13	123 min	Dramas	A brilliant group of students become card-coun...
netflix.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7787 entries, 0 to 7786
Data columns (total 12 columns):
 #   Column        Non-Null Count  Dtype 
---  ------        --------------  ----- 
 0   show_id       7787 non-null   object
 1   type          7787 non-null   object
 2   title         7787 non-null   object
 3   director      5398 non-null   object
 4   cast          7069 non-null   object
 5   country       7280 non-null   object
 6   date_added    7777 non-null   object
 7   release_year  7787 non-null   int64 
 8   rating        7780 non-null   object
 9   duration      7787 non-null   object
 10  listed_in     7787 non-null   object
 11  description   7787 non-null   object
dtypes: int64(1), object(11)
memory usage: 730.2+ KB
netflix.shape
(7787, 12)
netflix.isnull().sum()
show_id            0
type               0
title              0
director        2389
cast             718
country          507
date_added        10
release_year       0
rating             7
duration           0
listed_in          0
description        0
dtype: int64
netflix.nunique()
show_id         7787
type               2
title           7787
director        4049
cast            6831
country          681
date_added      1565
release_year      73
rating            14
duration         216
listed_in        492
description     7769
dtype: int64
**Type : Movies Or TV Shows

#Type : Movies or Tv Show
sns.countplot(netflix['type'],color='grey',orient='v')
plt.tight_layout()
/opt/conda/lib/python3.7/site-packages/seaborn/_decorators.py:43: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
  FutureWarning

netflix['type'].value_counts()
Movie      5377
TV Show    2410
Name: type, dtype: int64
pd.crosstab(netflix.release_year, netflix.type).plot(kind='bar',figsize=(15,15))
<AxesSubplot:xlabel='release_year'>

Release Year
  File "<ipython-input-11-967642327018>", line 1
    Release Year
               ^
SyntaxError: invalid syntax
#tahun realease
def release(release_date):
    if 1960<=release_date<=1990:
        return 'Very old'
    elif 1990<release_date<= 2000:
        return 'Old'
    elif 2000<release_date<=2015:
        return 'Early 21st century'
    elif 2015<release_date<=2021:
        return 'New'
    else:
        return None
netflix['Movie Release type']=netflix['release_year'].apply(release)
netflix
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description	Movie Release type
0	s1	TV Show	3%	NaN	João Miguel, Bianca Comparato, Michel Gomes, R...	Brazil	August 14, 2020	2020	TV-MA	4 Seasons	International TV Shows, TV Dramas, TV Sci-Fi &...	In a future where the elite inhabit an island ...	New
1	s2	Movie	7:19	Jorge Michel Grau	Demián Bichir, Héctor Bonilla, Oscar Serrano, ...	Mexico	December 23, 2016	2016	TV-MA	93 min	Dramas, International Movies	After a devastating earthquake hits Mexico Cit...	New
2	s3	Movie	23:59	Gilbert Chan	Tedd Chan, Stella Chung, Henley Hii, Lawrence ...	Singapore	December 20, 2018	2011	R	78 min	Horror Movies, International Movies	When an army recruit is found dead, his fellow...	Early 21st century
3	s4	Movie	9	Shane Acker	Elijah Wood, John C. Reilly, Jennifer Connelly...	United States	November 16, 2017	2009	PG-13	80 min	Action & Adventure, Independent Movies, Sci-Fi...	In a postapocalyptic world, rag-doll robots hi...	Early 21st century
4	s5	Movie	21	Robert Luketic	Jim Sturgess, Kevin Spacey, Kate Bosworth, Aar...	United States	January 1, 2020	2008	PG-13	123 min	Dramas	A brilliant group of students become card-coun...	Early 21st century
...	...	...	...	...	...	...	...	...	...	...	...	...	...
7782	s7783	Movie	Zozo	Josef Fares	Imad Creidi, Antoinette Turk, Elias Gergi, Car...	Sweden, Czech Republic, United Kingdom, Denmar...	October 19, 2020	2005	TV-MA	99 min	Dramas, International Movies	When Lebanon's Civil War deprives Zozo of his ...	Early 21st century
7783	s7784	Movie	Zubaan	Mozez Singh	Vicky Kaushal, Sarah-Jane Dias, Raaghav Chanan...	India	March 2, 2019	2015	TV-14	111 min	Dramas, International Movies, Music & Musicals	A scrappy but poor boy worms his way into a ty...	Early 21st century
7784	s7785	Movie	Zulu Man in Japan	NaN	Nasty C	NaN	September 25, 2020	2019	TV-MA	44 min	Documentaries, International Movies, Music & M...	In this documentary, South African rapper Nast...	New
7785	s7786	TV Show	Zumbo's Just Desserts	NaN	Adriano Zumbo, Rachel Khoo	Australia	October 31, 2020	2019	TV-PG	1 Season	International TV Shows, Reality TV	Dessert wizard Adriano Zumbo looks for the nex...	New
7786	s7787	Movie	ZZ TOP: THAT LITTLE OL' BAND FROM TEXAS	Sam Dunn	NaN	United Kingdom, Canada, United States	March 1, 2020	2019	TV-MA	90 min	Documentaries, Music & Musicals	This documentary delves into the mystique behi...	New
7787 rows × 13 columns

t=netflix.groupby('Movie Release type').type.value_counts()
t
Movie Release type  type   
Early 21st century  Movie      1820
                    TV Show     574
New                 Movie      3125
                    TV Show    1785
Old                 Movie       207
                    TV Show      32
Very old            Movie       201
                    TV Show      17
Name: type, dtype: int64
#plt.figure(figsize=(13,8))
sns.countplot(netflix['Movie Release type'][:],hue=netflix['type'],color='grey')
/opt/conda/lib/python3.7/site-packages/seaborn/_decorators.py:43: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
  FutureWarning
<AxesSubplot:xlabel='Movie Release type', ylabel='count'>

15 latest tv shows

netflix[netflix['type']=='TV Show'].sort_values('release_year').tail(15)
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description	Movie Release type
1864	s1865	TV Show	Dream Home Makeover	NaN	NaN	United States	January 1, 2021	2021	TV-G	2 Seasons	Reality TV	Dreams come true for real families looking for...	New
1780	s1781	TV Show	Disenchantment	NaN	Abbi Jacobson, Eric André, Nat Faxon, John DiM...	United States	January 15, 2021	2021	TV-14	3 Seasons	TV Action & Adventure, TV Comedies, TV Sci-Fi ...	Princess duties call, but she'd rather be drin...	New
2741	s2742	TV Show	Hilda	NaN	Bella Ramsey, Ameerah Falzon-Ojo, Oliver Nelso...	United Kingdom, Canada, United States	December 14, 2020	2021	TV-Y7	2 Seasons	Kids' TV	Fearless, free-spirited Hilda finds new friend...	New
2753	s2754	TV Show	History of Swear Words	NaN	Nicolas Cage	United States	January 5, 2021	2021	TV-MA	1 Season	Docuseries, TV Comedies	Nicolas Cage hosts this proudly profane, funny...	New
6477	s6478	TV Show	The Idhun Chronicles	Maite Ruiz De Austri	Michelle Jenner, Itzan Escamilla, Sergio Mur, ...	Spain	January 8, 2021	2021	TV-14	2 Seasons	Anime Series, International TV Shows, Spanish-...	A boy suddenly orphaned fights his parents' ki...	New
3018	s3019	TV Show	Inside the World’s Toughest Prisons	NaN	Paul Connolly	United Kingdom	January 8, 2021	2021	TV-MA	5 Seasons	British TV Shows, Crime TV Shows, Docuseries	Investigative journalist Paul Connolly becomes...	New
1440	s1441	TV Show	Cobra Kai	NaN	Ralph Macchio, William Zabka, Xolo Maridueña, ...	United States	January 1, 2021	2021	TV-14	3 Seasons	TV Action & Adventure, TV Dramas	Decades after the tournament that changed thei...	New
3822	s3823	TV Show	Lupin	NaN	Omar Sy, Ludivine Sagnier, Clotilde Hesme, Nic...	United States	January 8, 2021	2021	TV-MA	1 Season	Crime TV Shows, International TV Shows, TV Act...	Inspired by the adventures of Arsène Lupin, ge...	New
4086	s4087	TV Show	Mighty Little Bheem: Kite Festival	NaN	Sumruddhi Shukla, Aranya Kaur, Nishka Raheja	India	January 8, 2021	2021	TV-Y	1 Season	Kids' TV, TV Comedies	With winter behind them, Bheem and his townspe...	New
4173	s4174	TV Show	Monarca	NaN	Irene Azuela, Juan Manuel Bernal, Osvaldo Bena...	Mexico	January 1, 2021	2021	TV-MA	2 Seasons	International TV Shows, Spanish-Language TV Sh...	After 20 years, Ana María returns to Mexico an...	New
980	s981	TV Show	Bling Empire	NaN	NaN	NaN	January 15, 2021	2021	TV-MA	1 Season	Reality TV	Follow LA's wildly wealthy Asian and Asian Ame...	New
5921	s5922	TV Show	Surviving Death	NaN	NaN	United States	January 6, 2021	2021	TV-MA	1 Season	Docuseries, Reality TV	What happens after we die? This docuseries exp...	New
4390	s4391	TV Show	Nailed It! Mexico	NaN	Omar Chaparro, Anna Ruiz	Mexico, United States	January 5, 2021	2021	TV-PG	3 Seasons	International TV Shows, Reality TV, Spanish-La...	The fun, fondant and hilarious cake fails head...	New
4965	s4966	TV Show	Pretend It’s a City	NaN	Fran Lebowitz	United States	January 8, 2021	2021	TV-14	1 Season	Docuseries	Wander the New York City streets and fascinati...	New
2672	s2673	TV Show	Headspace Guide to Meditation	NaN	Andy Puddicombe	United States	January 1, 2021	2021	TV-G	1 Season	Docuseries, Science & Nature TV	Headspace takes a friendly, animated look at t...	New
netflix[netflix['type']=='Movie'].sort_values('release_year').tail(15)
show_id	type	title	director	cast	country	date_added	release_year	rating	duration	listed_in	description	Movie Release type
525	s526	Movie	Angu Vaikuntapurathu (Malayalam)	Trivikram Srinivas	Allu Arjun, Pooja Hegde, Tabu, Sushanth, Nivet...	NaN	March 5, 2020	2020	TV-14	162 min	Action & Adventure, Comedies, Dramas	After growing up enduring criticism from his f...	New
5279	s5280	Movie	Rooting for Roona	Pavitra Chalam, Akshay Shankar	NaN	India	October 15, 2020	2020	TV-PG	42 min	Documentaries, International Movies	In rural India, a child with hydrocephalus get...	New
520	s521	Movie	Angela's Christmas Wish	Damien O’Connor	Lucy O'Connell, Brendan Mullins, Ruth Negga, L...	United States	December 1, 2020	2020	TV-Y	48 min	Children & Family Movies	With her father working far away in Australia,...	New
7551	s7552	Movie	What Happened to Mr. Cha?	Kim Dong-kyu	Cha In-pyo, Cho Dal-hwan, Song Jae-ryong	South Korea	January 1, 2021	2021	TV-MA	102 min	Comedies, International Movies	With the peak of his career long behind him, a...	New
7220	s7221	Movie	Tribhanga - Tedhi Medhi Crazy	Renuka Shahane	Kajol, Tanvi Azmi, Mithila Palkar, Kunaal Roy ...	NaN	January 15, 2021	2021	TV-MA	96 min	Dramas, International Movies	When her estranged mother falls into a coma, a...	New
1285	s1286	Movie	Charming	Ross Venokur	Wilmer Valderrama, Demi Lovato, Sia, Nia Varda...	Canada, United States, Cayman Islands	January 8, 2021	2021	TV-Y7	85 min	Children & Family Movies, Comedies	On the eve of his 21st birthday, an adored pri...	New
5859	s5860	Movie	Stuck Apart	NaN	Engin Günaydın, Haluk Bilginer, Binnur Kaya, Ö...	Turkey	January 8, 2021	2021	TV-MA	97 min	Comedies, Dramas, International Movies	Entrenched in a midlife crisis, Aziz seeks sol...	New
6670	s6671	Movie	The Minimalists: Less Is Now	NaN	NaN	United States	January 1, 2021	2021	TV-14	54 min	Documentaries	They've built a movement out of minimalism. Lo...	New
1528	s1529	Movie	Creating The Queen's Gambit	NaN	NaN	NaN	January 8, 2021	2021	TV-14	14 min	Documentaries	A fascinating character. Exquisite sets. A wig...	New
7569	s7570	Movie	What Would Sophia Loren Do?	Ross Kauffman	Nancy "Vincenza Careri" Kulik, Sophia Loren	United States	January 15, 2021	2021	TV-14	32 min	Documentaries	In this delightful short documentary, an Itali...	New
7644	s7645	Movie	Wish You	Sung Do-jun	Kang In-soo, Lee Sang, Soo-bin	NaN	January 15, 2021	2021	TV-PG	102 min	Dramas, International Movies, LGBTQ Movies	Singing and dreaming together, a talented sing...	New
1514	s1515	Movie	Crack: Cocaine, Corruption & Conspiracy	Stanley Nelson	NaN	United States	January 11, 2021	2021	TV-MA	90 min	Documentaries	A cheap, powerful drug emerges during a recess...	New
4710	s4711	Movie	Outside the Wire	Mikael Håfström	Anthony Mackie, Damson Idris, Emily Beecham, M...	NaN	January 15, 2021	2021	R	116 min	Action & Adventure	In the near future, a drone pilot sent into a ...	New
5103	s5104	Movie	Ratones Paranoicos: The Band that Rocked Argen...	Alejandro Ruax, Ramiro Martínez	Juan Sebastián Gutiérrez, Pablo Cano, Pablo Me...	NaN	January 6, 2021	2021	TV-MA	76 min	Documentaries, International Movies, Music & M...	The irrepressible Ratones Paranoicos, Argentin...	New
1355	s1356	Movie	Chris Rock Total Blackout: The Tamborine Exten...	Chris Rock	Chris Rock	NaN	January 12, 2021	2021	TV-MA	98 min	Stand-Up Comedy	In this extended cut of his 2018 special, Chri...	New
Rating

netflix.groupby('rating').type.value_counts()
rating    type   
G         Movie        39
NC-17     Movie         3
NR        Movie        79
          TV Show       5
PG        Movie       247
PG-13     Movie       386
R         Movie       663
          TV Show       2
TV-14     Movie      1272
          TV Show     659
TV-G      Movie       111
          TV Show      83
TV-MA     Movie      1845
          TV Show    1018
TV-PG     Movie       505
          TV Show     301
TV-Y      TV Show     163
          Movie       117
TV-Y7     TV Show     176
          Movie        95
TV-Y7-FV  Movie         5
          TV Show       1
UR        Movie         5
Name: type, dtype: int64
plt.figure(figsize=(13,8))
sns.countplot(netflix['rating'][:],hue=netflix['type'],color='Purple')
/opt/conda/lib/python3.7/site-packages/seaborn/_decorators.py:43: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
  FutureWarning
<AxesSubplot:xlabel='rating', ylabel='count'>

Country

x= netflix['country'].value_counts().head(20)
x
United States                    2555
India                             923
United Kingdom                    397
Japan                             226
South Korea                       183
Canada                            177
Spain                             134
France                            115
Egypt                             101
Turkey                            100
Mexico                            100
Australia                          83
Taiwan                             78
Brazil                             72
Philippines                        71
Nigeria                            70
Indonesia                          70
United Kingdom, United States      64
Germany                            61
United States, Canada              60
Name: country, dtype: int64
sns.barplot(x=x.values,y=x.index)
<AxesSubplot:>

print('10 Negara Top Movie')
netflix.groupby('type').country.value_counts()['Movie'][:10]
10 Negara Top Movie
country
United States     1850
India              852
United Kingdom     193
Canada             118
Egypt               89
Spain               89
Turkey              73
Philippines         70
France              69
Japan               69
Name: country, dtype: int64
print('10 Top TV Show')
netflix.groupby('type').country.value_counts()['TV Show'][:10]
10 Top TV Show
country
United States     705
United Kingdom    204
Japan             157
South Korea       147
India              71
Taiwan             68
Canada             59
Australia          46
France             46
Spain              45
Name: country, dtype: int64
Listed In

n= netflix['listed_in'].value_counts()[:20]
n
Documentaries                                        334
Stand-Up Comedy                                      321
Dramas, International Movies                         320
Comedies, Dramas, International Movies               243
Dramas, Independent Movies, International Movies     215
Kids' TV                                             205
Children & Family Movies                             177
Documentaries, International Movies                  172
Children & Family Movies, Comedies                   169
Comedies, International Movies                       161
Dramas, International Movies, Romantic Movies        153
Comedies, International Movies, Romantic Movies      139
Action & Adventure, Dramas, International Movies     117
Dramas                                               117
International TV Shows, TV Dramas                    111
Dramas, International Movies, Thrillers              109
Crime TV Shows, International TV Shows, TV Dramas    106
Comedies, Dramas, Independent Movies                 101
Action & Adventure                                    99
Comedies                                              97
Name: listed_in, dtype: int64
sns.barplot(x=n.values,y=n.index)
<AxesSubplot:>

Duration And Session

l=[]
m=[]

for i in netflix['duration']:
    if i[3:6]=='min':
        l.append(int(i[0:2]))
    elif i[4:7]=='min':
        l.append(int(i[0:3]))
    elif i[3:10]=='Season':
        m.append(int(i[0:2]))

#durasi movie dalam menit
plt.figure(figsize=(12,6))
sns.set_style('darkgrid')
sns.distplot(l)
plt.xlabel('time in minutes')
plt.ylabel('% of netflix movies')
plt.title('Duration distribution of movies on netflix(in minute)')
  l=[]
m=[]

for i in netflix['duration']:
    if i[3:6]=='min':
        l.append(int(i[0:2]))
    elif i[4:7]=='min':
        l.append(int(i[0:3]))
    elif i[3:10]=='Seasons':
        m.append(int(i[0:2]))

plt.figure(figsize=(12,6))
sns.countplot(m)
plt.xlabel('No of Season')
plt.ylabel('% of netflix TV Shows')
plt.title('Duration distribution of movies on netflix(no of season')
  #Movie
netflix.groupby('type').director.value_counts()['Movie'][:10].plot(kind='bar')
  #TV Show
netflix.groupby('type').director.value_counts()['TV Show'][:10].plot(kind='bar')
