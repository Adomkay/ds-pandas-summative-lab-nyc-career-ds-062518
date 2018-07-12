
# Pandas Summative Lab

## Problem Statement
In this lab, we'll make use of everything we've learned about pandas, data cleaning, and Exploratory Data Analysis. 

### The Dataset
In this lab, we'll work with the comprehensive [Super Heroes Dataset](https://www.kaggle.com/claudiodavi/superhero-set/data), which can be found on Kaggle!

### Objectives
* Use all available pandas knowledge to clean the dataset and deal with null values
* Use Queries and aggregations to group the data into interesting subsets as needed
* Use descriptive statistics and data visualization to find answers to questions we may have about the data.  



```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
pd.options.display.max_rows = 1000
%matplotlib inline
```

For this lab, our dataset is split among two different sources--`heroes_information.csv` and `super_hero_powers.csv`.

Use pandas to read in each file and store them in DataFrames in the appropriate variables below. Then, display the head of each to ensure that everything loaded correctly.  


```python
heroes_df = pd.read_csv('heroes_information.csv')
powers_df = pd.read_csv('super_hero_powers.csv')
display(heroes_df.head())
powers_df.head()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>name</th>
      <th>Gender</th>
      <th>Eye color</th>
      <th>Race</th>
      <th>Hair color</th>
      <th>Height</th>
      <th>Publisher</th>
      <th>Skin color</th>
      <th>Alignment</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A-Bomb</td>
      <td>Male</td>
      <td>yellow</td>
      <td>Human</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>good</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Abe Sapien</td>
      <td>Male</td>
      <td>blue</td>
      <td>Icthyo Sapien</td>
      <td>No Hair</td>
      <td>191.0</td>
      <td>Dark Horse Comics</td>
      <td>blue</td>
      <td>good</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Abin Sur</td>
      <td>Male</td>
      <td>blue</td>
      <td>Ungaran</td>
      <td>No Hair</td>
      <td>185.0</td>
      <td>DC Comics</td>
      <td>red</td>
      <td>good</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Abomination</td>
      <td>Male</td>
      <td>green</td>
      <td>Human / Radiation</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Abraxas</td>
      <td>Male</td>
      <td>blue</td>
      <td>Cosmic Entity</td>
      <td>Black</td>
      <td>-99.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>-99.0</td>
    </tr>
  </tbody>
</table>
</div>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hero_names</th>
      <th>Agility</th>
      <th>Accelerated Healing</th>
      <th>Lantern Power Ring</th>
      <th>Dimensional Awareness</th>
      <th>Cold Resistance</th>
      <th>Durability</th>
      <th>Stealth</th>
      <th>Energy Absorption</th>
      <th>Flight</th>
      <th>...</th>
      <th>Web Creation</th>
      <th>Reality Warping</th>
      <th>Odin Force</th>
      <th>Symbiote Costume</th>
      <th>Speed Force</th>
      <th>Phoenix Force</th>
      <th>Molecular Dissipation</th>
      <th>Vision - Cryo</th>
      <th>Omnipresent</th>
      <th>Omniscient</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3-D Man</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A-Bomb</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Abe Sapien</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Abin Sur</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Abomination</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 168 columns</p>
</div>



It looks as if the heroes information dataset contained an index column.  We did not specify that this dataset contained an index column, because we hadn't seen it yet. Pandas does not know how to tell apart an index column from any other data, so it stored it with the column name `Unnamed: 0`.  

Our DataFrame provided row indices by default, so this column is not needed.  Drop it from the DataFrame in place in the cell below, and then display the head of `heroes_df` to ensure that it worked properly. 


```python
heroes_df.drop('Unnamed: 0', axis=1, inplace=True)
heroes_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>Gender</th>
      <th>Eye color</th>
      <th>Race</th>
      <th>Hair color</th>
      <th>Height</th>
      <th>Publisher</th>
      <th>Skin color</th>
      <th>Alignment</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A-Bomb</td>
      <td>Male</td>
      <td>yellow</td>
      <td>Human</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>good</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Abe Sapien</td>
      <td>Male</td>
      <td>blue</td>
      <td>Icthyo Sapien</td>
      <td>No Hair</td>
      <td>191.0</td>
      <td>Dark Horse Comics</td>
      <td>blue</td>
      <td>good</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Abin Sur</td>
      <td>Male</td>
      <td>blue</td>
      <td>Ungaran</td>
      <td>No Hair</td>
      <td>185.0</td>
      <td>DC Comics</td>
      <td>red</td>
      <td>good</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Abomination</td>
      <td>Male</td>
      <td>green</td>
      <td>Human / Radiation</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Abraxas</td>
      <td>Male</td>
      <td>blue</td>
      <td>Cosmic Entity</td>
      <td>Black</td>
      <td>-99.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>-99.0</td>
    </tr>
  </tbody>
</table>
</div>



### Familiarize Yourself With the Dataset

The first step in our Exploratory Data Analysis will be to get familiar with the data.  This step includes:

* Understanding the dimensionality of your dataset
* Investigating what type of data it contains, and the data types used to store it
* Discovering how missing values are encoded, and how many there are
* Getting a feel for what information it does and doesnt contain

In the cell below, get the descriptive statistics of each DataFrame.  


```python
display(heroes_df.describe())
powers_df.describe()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Height</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>734.000000</td>
      <td>732.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>102.254087</td>
      <td>43.855191</td>
    </tr>
    <tr>
      <th>std</th>
      <td>139.624543</td>
      <td>130.823733</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-99.000000</td>
      <td>-99.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-99.000000</td>
      <td>-99.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>175.000000</td>
      <td>62.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>185.000000</td>
      <td>90.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>975.000000</td>
      <td>900.000000</td>
    </tr>
  </tbody>
</table>
</div>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hero_names</th>
      <th>Agility</th>
      <th>Accelerated Healing</th>
      <th>Lantern Power Ring</th>
      <th>Dimensional Awareness</th>
      <th>Cold Resistance</th>
      <th>Durability</th>
      <th>Stealth</th>
      <th>Energy Absorption</th>
      <th>Flight</th>
      <th>...</th>
      <th>Web Creation</th>
      <th>Reality Warping</th>
      <th>Odin Force</th>
      <th>Symbiote Costume</th>
      <th>Speed Force</th>
      <th>Phoenix Force</th>
      <th>Molecular Dissipation</th>
      <th>Vision - Cryo</th>
      <th>Omnipresent</th>
      <th>Omniscient</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>...</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
      <td>667</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>667</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Moses Magnum</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1</td>
      <td>425</td>
      <td>489</td>
      <td>656</td>
      <td>642</td>
      <td>620</td>
      <td>410</td>
      <td>541</td>
      <td>590</td>
      <td>455</td>
      <td>...</td>
      <td>653</td>
      <td>651</td>
      <td>665</td>
      <td>658</td>
      <td>666</td>
      <td>666</td>
      <td>666</td>
      <td>665</td>
      <td>665</td>
      <td>665</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 168 columns</p>
</div>



### Dealing with Null Values

Starting in the cell below, detect and deal with any null values in either data frame.  Then, explain your methodology for detecting and dealing with outliers in the markdown section below.  Be sure to explain your strategy for dealing with null values in numeric columns, as well as your strategy for dealing with null values in non-numeric columns.  

Note that if you need to add more cells to write code in, you can do this by:

**1.** Highlighting a cell and then pressing `ESC` to enter command mode.  
**2.** Press `A` to add a cell above the highlighted cell, or `B` to add a cell below the highlighted cell. 

Describe your strategy below this line:
____________________________________________________________________________________________________________________________

The `Weight` and `Publisher` columns contain null values.  Student should replace null values in `Weight` column with mean or median value for this column.  Since `Publisher` is a categorical column, having null values here is not necessarily a blocking problem.  We can either remove those rows (not desirable, because those rows might be interesting, and we should never throw away data when we can help it), we can leave them as is, or, since it is only 15 values, we could always look it up manually and fill in the correct values.  This is not expected for this lab, but would be a good solution if this data was important in a real-world project.   



```python
heroes_df.isna().any()
```




    name          False
    Gender        False
    Eye color     False
    Race          False
    Hair color    False
    Height        False
    Publisher      True
    Skin color    False
    Alignment     False
    Weight         True
    dtype: bool




```python
powers_df.isna().any()
```




    hero_names                      False
    Agility                         False
    Accelerated Healing             False
    Lantern Power Ring              False
    Dimensional Awareness           False
    Cold Resistance                 False
    Durability                      False
    Stealth                         False
    Energy Absorption               False
    Flight                          False
    Danger Sense                    False
    Underwater breathing            False
    Marksmanship                    False
    Weapons Master                  False
    Power Augmentation              False
    Animal Attributes               False
    Longevity                       False
    Intelligence                    False
    Super Strength                  False
    Cryokinesis                     False
    Telepathy                       False
    Energy Armor                    False
    Energy Blasts                   False
    Duplication                     False
    Size Changing                   False
    Density Control                 False
    Stamina                         False
    Astral Travel                   False
    Audio Control                   False
    Dexterity                       False
    Omnitrix                        False
    Super Speed                     False
    Possession                      False
    Animal Oriented Powers          False
    Weapon-based Powers             False
    Electrokinesis                  False
    Darkforce Manipulation          False
    Death Touch                     False
    Teleportation                   False
    Enhanced Senses                 False
    Telekinesis                     False
    Energy Beams                    False
    Magic                           False
    Hyperkinesis                    False
    Jump                            False
    Clairvoyance                    False
    Dimensional Travel              False
    Power Sense                     False
    Shapeshifting                   False
    Peak Human Condition            False
    Immortality                     False
    Camouflage                      False
    Element Control                 False
    Phasing                         False
    Astral Projection               False
    Electrical Transport            False
    Fire Control                    False
    Projection                      False
    Summoning                       False
    Enhanced Memory                 False
    Reflexes                        False
    Invulnerability                 False
    Energy Constructs               False
    Force Fields                    False
    Self-Sustenance                 False
    Anti-Gravity                    False
    Empathy                         False
    Power Nullifier                 False
    Radiation Control               False
    Psionic Powers                  False
    Elasticity                      False
    Substance Secretion             False
    Elemental Transmogrification    False
    Technopath/Cyberpath            False
    Photographic Reflexes           False
    Seismic Power                   False
    Animation                       False
    Precognition                    False
    Mind Control                    False
    Fire Resistance                 False
    Power Absorption                False
    Enhanced Hearing                False
    Nova Force                      False
    Insanity                        False
    Hypnokinesis                    False
    Animal Control                  False
    Natural Armor                   False
    Intangibility                   False
    Enhanced Sight                  False
    Molecular Manipulation          False
    Heat Generation                 False
    Adaptation                      False
    Gliding                         False
    Power Suit                      False
    Mind Blast                      False
    Probability Manipulation        False
    Gravity Control                 False
    Regeneration                    False
    Light Control                   False
    Echolocation                    False
    Levitation                      False
    Toxin and Disease Control       False
    Banish                          False
    Energy Manipulation             False
    Heat Resistance                 False
    Natural Weapons                 False
    Time Travel                     False
    Enhanced Smell                  False
    Illusions                       False
    Thirstokinesis                  False
    Hair Manipulation               False
    Illumination                    False
    Omnipotent                      False
    Cloaking                        False
    Changing Armor                  False
    Power Cosmic                    False
    Biokinesis                      False
    Water Control                   False
    Radiation Immunity              False
    Vision - Telescopic             False
    Toxin and Disease Resistance    False
    Spatial Awareness               False
    Energy Resistance               False
    Telepathy Resistance            False
    Molecular Combustion            False
    Omnilingualism                  False
    Portal Creation                 False
    Magnetism                       False
    Mind Control Resistance         False
    Plant Control                   False
    Sonar                           False
    Sonic Scream                    False
    Time Manipulation               False
    Enhanced Touch                  False
    Magic Resistance                False
    Invisibility                    False
    Sub-Mariner                     False
    Radiation Absorption            False
    Intuitive aptitude              False
    Vision - Microscopic            False
    Melting                         False
    Wind Control                    False
    Super Breath                    False
    Wallcrawling                    False
    Vision - Night                  False
    Vision - Infrared               False
    Grim Reaping                    False
    Matter Absorption               False
    The Force                       False
    Resurrection                    False
    Terrakinesis                    False
    Vision - Heat                   False
    Vitakinesis                     False
    Radar Sense                     False
    Qwardian Power Ring             False
    Weather Control                 False
    Vision - X-Ray                  False
    Vision - Thermal                False
    Web Creation                    False
    Reality Warping                 False
    Odin Force                      False
    Symbiote Costume                False
    Speed Force                     False
    Phoenix Force                   False
    Molecular Dissipation           False
    Vision - Cryo                   False
    Omnipresent                     False
    Omniscient                      False
    dtype: bool




```python
mean_weight = np.mean(heroes_df.Weight)
heroes_df['Weight'].fillna(mean_weight, inplace=True)
heroes_df.isna().sum()
```




    name           0
    Gender         0
    Eye color      0
    Race           0
    Hair color     0
    Height         0
    Publisher     15
    Skin color     0
    Alignment      0
    Weight         0
    dtype: int64



### Joining, Grouping, and Aggregating

In the cell below, join the two DataFrames.  Think about which sort of join you should use, as well as which columns you should join on.  Rename columns and manipulate as needed.  

**_HINT:_** If the join throws an error message, consider setting the the column you want to join on as the index for each DataFrame.  


```python
powers_df.rename(columns={'hero_names':'name'}, inplace=True)
```


```python
powers_df  = powers_df.astype('str')
```


```python
heroes_and_powers_df = powers_df.set_index('name').join(heroes_df.set_index('name'), how='inner')
heroes_and_powers_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Agility</th>
      <th>Accelerated Healing</th>
      <th>Lantern Power Ring</th>
      <th>Dimensional Awareness</th>
      <th>Cold Resistance</th>
      <th>Durability</th>
      <th>Stealth</th>
      <th>Energy Absorption</th>
      <th>Flight</th>
      <th>Danger Sense</th>
      <th>...</th>
      <th>Omniscient</th>
      <th>Gender</th>
      <th>Eye color</th>
      <th>Race</th>
      <th>Hair color</th>
      <th>Height</th>
      <th>Publisher</th>
      <th>Skin color</th>
      <th>Alignment</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A-Bomb</th>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>Male</td>
      <td>yellow</td>
      <td>Human</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>good</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>Abe Sapien</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>Male</td>
      <td>blue</td>
      <td>Icthyo Sapien</td>
      <td>No Hair</td>
      <td>191.0</td>
      <td>Dark Horse Comics</td>
      <td>blue</td>
      <td>good</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>Abin Sur</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>Male</td>
      <td>blue</td>
      <td>Ungaran</td>
      <td>No Hair</td>
      <td>185.0</td>
      <td>DC Comics</td>
      <td>red</td>
      <td>good</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>Abomination</th>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>Male</td>
      <td>green</td>
      <td>Human / Radiation</td>
      <td>No Hair</td>
      <td>203.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>441.0</td>
    </tr>
    <tr>
      <th>Abraxas</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>Male</td>
      <td>blue</td>
      <td>Cosmic Entity</td>
      <td>Black</td>
      <td>-99.0</td>
      <td>Marvel Comics</td>
      <td>-</td>
      <td>bad</td>
      <td>-99.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 176 columns</p>
</div>




```python
heroes_and_powers_df.isna().sum()
```




    Agility                          0
    Accelerated Healing              0
    Lantern Power Ring               0
    Dimensional Awareness            0
    Cold Resistance                  0
    Durability                       0
    Stealth                          0
    Energy Absorption                0
    Flight                           0
    Danger Sense                     0
    Underwater breathing             0
    Marksmanship                     0
    Weapons Master                   0
    Power Augmentation               0
    Animal Attributes                0
    Longevity                        0
    Intelligence                     0
    Super Strength                   0
    Cryokinesis                      0
    Telepathy                        0
    Energy Armor                     0
    Energy Blasts                    0
    Duplication                      0
    Size Changing                    0
    Density Control                  0
    Stamina                          0
    Astral Travel                    0
    Audio Control                    0
    Dexterity                        0
    Omnitrix                         0
    Super Speed                      0
    Possession                       0
    Animal Oriented Powers           0
    Weapon-based Powers              0
    Electrokinesis                   0
    Darkforce Manipulation           0
    Death Touch                      0
    Teleportation                    0
    Enhanced Senses                  0
    Telekinesis                      0
    Energy Beams                     0
    Magic                            0
    Hyperkinesis                     0
    Jump                             0
    Clairvoyance                     0
    Dimensional Travel               0
    Power Sense                      0
    Shapeshifting                    0
    Peak Human Condition             0
    Immortality                      0
    Camouflage                       0
    Element Control                  0
    Phasing                          0
    Astral Projection                0
    Electrical Transport             0
    Fire Control                     0
    Projection                       0
    Summoning                        0
    Enhanced Memory                  0
    Reflexes                         0
    Invulnerability                  0
    Energy Constructs                0
    Force Fields                     0
    Self-Sustenance                  0
    Anti-Gravity                     0
    Empathy                          0
    Power Nullifier                  0
    Radiation Control                0
    Psionic Powers                   0
    Elasticity                       0
    Substance Secretion              0
    Elemental Transmogrification     0
    Technopath/Cyberpath             0
    Photographic Reflexes            0
    Seismic Power                    0
    Animation                        0
    Precognition                     0
    Mind Control                     0
    Fire Resistance                  0
    Power Absorption                 0
    Enhanced Hearing                 0
    Nova Force                       0
    Insanity                         0
    Hypnokinesis                     0
    Animal Control                   0
    Natural Armor                    0
    Intangibility                    0
    Enhanced Sight                   0
    Molecular Manipulation           0
    Heat Generation                  0
    Adaptation                       0
    Gliding                          0
    Power Suit                       0
    Mind Blast                       0
    Probability Manipulation         0
    Gravity Control                  0
    Regeneration                     0
    Light Control                    0
    Echolocation                     0
    Levitation                       0
    Toxin and Disease Control        0
    Banish                           0
    Energy Manipulation              0
    Heat Resistance                  0
    Natural Weapons                  0
    Time Travel                      0
    Enhanced Smell                   0
    Illusions                        0
    Thirstokinesis                   0
    Hair Manipulation                0
    Illumination                     0
    Omnipotent                       0
    Cloaking                         0
    Changing Armor                   0
    Power Cosmic                     0
    Biokinesis                       0
    Water Control                    0
    Radiation Immunity               0
    Vision - Telescopic              0
    Toxin and Disease Resistance     0
    Spatial Awareness                0
    Energy Resistance                0
    Telepathy Resistance             0
    Molecular Combustion             0
    Omnilingualism                   0
    Portal Creation                  0
    Magnetism                        0
    Mind Control Resistance          0
    Plant Control                    0
    Sonar                            0
    Sonic Scream                     0
    Time Manipulation                0
    Enhanced Touch                   0
    Magic Resistance                 0
    Invisibility                     0
    Sub-Mariner                      0
    Radiation Absorption             0
    Intuitive aptitude               0
    Vision - Microscopic             0
    Melting                          0
    Wind Control                     0
    Super Breath                     0
    Wallcrawling                     0
    Vision - Night                   0
    Vision - Infrared                0
    Grim Reaping                     0
    Matter Absorption                0
    The Force                        0
    Resurrection                     0
    Terrakinesis                     0
    Vision - Heat                    0
    Vitakinesis                      0
    Radar Sense                      0
    Qwardian Power Ring              0
    Weather Control                  0
    Vision - X-Ray                   0
    Vision - Thermal                 0
    Web Creation                     0
    Reality Warping                  0
    Odin Force                       0
    Symbiote Costume                 0
    Speed Force                      0
    Phoenix Force                    0
    Molecular Dissipation            0
    Vision - Cryo                    0
    Omnipresent                      0
    Omniscient                       0
    Gender                           0
    Eye color                        0
    Race                             0
    Hair color                       0
    Height                           0
    Publisher                       13
    Skin color                       0
    Alignment                        0
    Weight                           0
    dtype: int64



In the cell below, subset male and female heroes into different dataframes.  Create a scatterplot of the height and weight of each hero, with weight as the y-axis.  Plot both the male and female heroes subset into each dataframe, and make the color for each point in the scatterplot correspond to the gender of the superhero.


```python
male_heroes_df = heroes_df[heroes_df['Gender'] == 'Male']
female_heroes_df = heroes_df[heroes_df['Gender'] == 'Female']

plt.figure(figsize=(10, 7))
m = plt.scatter(male_heroes_df.Weight, male_heroes_df.Height, color='b')
f = plt.scatter(female_heroes_df.Weight, female_heroes_df.Height, color='r')
plt.legend((m, f), ('Male', 'Female'))
plt.xlabel('Weight')
plt.ylabel('Height')
plt.title("Heroes by Weight and Height")
```




    Text(0.5,1,'Heroes by Weight and Height')




![png](output_18_1.png)


Next, slice the DataFrame as needed and visualize the distribution of heights and weights by gender.  You should have 4 total plots.  


```python


def show_distplot(dataframe, gender, column_name):
    plt.plot()
    sns.distplot(dataframe[column_name])
    plt.title("Distribution of {} for {} heroes".format(column_name, gender))
    plt.xlabel(column_name)
    plt.ylabel("Probability Density")
    plt.show()
```


```python
# Male Height
show_distplot(heroes_and_powers_df, 'Male', 'Height')
print("Mean Height for male heroes: {}".format(np.mean(male_heroes_df.Height)))
print("Median Height for male heroes: {}".format(np.median(male_heroes_df.Height)))
```


![png](output_21_0.png)


    Mean Height for male heroes: 107.27524752475247
    Median Height for male heroes: 180.0
    


```python
# Male Weight
show_distplot(heroes_and_powers_df, 'Male', 'Weight')
print("Mean weight for male heroes: {}".format(np.mean(male_heroes_df.Weight)))
print("Median weight for male heroes: {}".format(np.median(male_heroes_df.Weight)))
```


![png](output_22_0.png)


    Mean weight for male heroes: 52.03535681436996
    Median weight for male heroes: 79.0
    


```python
# Female Height
show_distplot(heroes_and_powers_df, 'Female', 'Height')
print("Mean weight for female heroes: {}".format(np.mean(male_heroes_df.Height)))
print("Median weight for female heroes: {}".format(np.median(male_heroes_df.Height)))
```


![png](output_23_0.png)


    Mean weight for female heroes: 107.27524752475247
    Median weight for female heroes: 180.0
    


```python
# Female Weight
show_distplot(heroes_and_powers_df, 'Female', 'Weight')
print("Mean weight for female heroes: {}".format(np.mean(female_heroes_df.Weight)))
print("Median weight for female heroes: {}".format(np.median(male_heroes_df.Weight)))
```


![png](output_24_0.png)


    Mean weight for female heroes: 27.265
    Median weight for female heroes: 79.0
    

Discuss your findings from the plots above, with respect to the distibution of height and weight by gender.  Your explanation should include discussion of any relevant summary statistics, including mean, median, mode, and the overall shape of each distribution.  

Wite your answer below this line:
____________________________________________________________________________________________________________________________

Answer should notice that every single distribution is bimodal, and each contains huge outliers.  Strong variability in each distribution.  Student should do more than just plot these, since they'll need to access the mean and median for each distribution as well.  Student should also consider comparing the descriptive statistics from each distribution.  

### Sample Question: Most Common Powers

The rest of this notebook will be left to you to investigate the dataset by formulating your own questions, and then seeking answers using pandas and numpy.  Every answer should include some sort of visualization, when appropriate. Before moving on to formulating your own questions, use the dataset to answer the following questions about superhero powers:

* What are the 5 most common powers overall?
* What are the 5 most common powers in the Marvel Universe?
* What are the 5 most common powers in the DC Universe?


```python
def top_5_powers(dataframe):
    df = dataframe.drop(heroes_df.columns.values[1:], axis=1)
    columns = df.columns.values
    for col in columns:
        df[col] = df[col].map({"True": 1, "False": 0})
        
    power_counts_dict = dict(df.sum())
    
    return sorted(power_counts_dict.items(), key=lambda x: x[1], reverse=True)[:5] 
    
overall_top_5 = top_5_powers(heroes_and_powers_df)
marvel_df = heroes_and_powers_df[heroes_and_powers_df['Publisher'] == 'Marvel Comics']
dc_df = heroes_and_powers_df[heroes_and_powers_df['Publisher'] == 'DC Comics']
print(overall_top_5)
```

    [('Super Strength', 362), ('Stamina', 294), ('Durability', 262), ('Super Speed', 251), ('Agility', 244)]
    


```python
marvel_top_5 = top_5_powers(marvel_df)
print(marvel_top_5)
```

    [('Super Strength', 204), ('Durability', 154), ('Stamina', 150), ('Super Speed', 137), ('Agility', 126)]
    


```python
dc_top_5 = top_5_powers(dc_df)
print(dc_top_5)
```

    [('Super Strength', 109), ('Stamina', 90), ('Flight', 86), ('Super Speed', 79), ('Agility', 71)]
    


```python
def top_5_bar_chart(top_5_list, publisher=None):
    marvel_powers = [i[0] for i in top_5_list]
    marvel_values = [i[1] for i in top_5_list]

    plt.clf()
    plt.figure(figsize=(10, 7))
    plt.bar(marvel_powers, marvel_values)
    if publisher:
        plt.title("Top 5 Powers in {} Universe".format(publisher))
    else:
        plt.title("Top 5 Powers in Superheroes Dataset")
    plt.show()

display(top_5_bar_chart(overall_top_5))
display(top_5_bar_chart(dc_top_5, publisher="DC Comics"))
top_5_bar_chart(marvel_top_5, publisher="Marvel Comics")
    
```


    <matplotlib.figure.Figure at 0x251025dbf60>



![png](output_30_1.png)



    None



    <matplotlib.figure.Figure at 0x25102781ac8>



![png](output_30_4.png)



    None



    <matplotlib.figure.Figure at 0x25102630208>



![png](output_30_7.png)


Analyze the results you found above to answer the following question:

How do the top 5 powers in the Marvel and DC universes compare?  Are they similar, or are there significant differences? How do they compare to the overall trends in the entire Superheroes dataset?

Wite your answer below this line:
____________________________________________________________________________________________________________________________
The top 5 powers are largely similar for each of the 3 groups, with the exception being flight in the DC universe, which differs from durability as seen in both the overall dataset and the marvel universe subset.  Super Strength is the most common in each.

### Your Own Investigation

For the remainder of this lab, you'll be focusing on coming up with and answering your own question, just like we did above.  Your question should not be overly simple, and should require both descriptive statistics and data visualization to answer.  In case you're unsure of what questions to ask, some sample questions have been provided below.

Pick one of the following questions to investigate and answer, or come up with one of your own!

* Which powers have the highest chance of co-occuring in a hero (e.g. super strength and flight), and does this differ by gender?
* Is there a relationship between a hero's height and weight and their powerset?
* What is the distribution of skin colors amongst alien heroes?

Explain your question below this line:
____________________________________________________________________________________________________________________________



Some sample cells have been provided to give you room to work. If you need to create more cells, you can do this easily by:

1. Highlighting a cell and then pressing `esc` to enter command mode.
1. Pressing `b` to add a cell below the currently highlighted cell, or `a` to add one above it.  

Be sure to include thoughtful, well-labeled visualizations to back up your analysis!

# Conclusion

In this lab, we demonstrated our mastery of:
* Use all available pandas knowledge to clean the dataset and deal with null values
* Use Queries and aggregations to group the data into interesting subsets as needed
* Use descriptive statistics and data visualization to find answers to questions we may have about the data.
