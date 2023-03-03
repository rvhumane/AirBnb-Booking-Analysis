# AirBnb-Booking-Analysis

# Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from google.colab import drive
drive.mount('/content/drive')

path='/content/Airbnb NYC 2019.csv'
airbnb_df = pd.read_csv(path)
