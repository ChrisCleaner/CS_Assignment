Our important papers:
MCC Van Dyke et al., 2019
JT Harvey, Applied Ergonomics, 2002
DW Ziegler et al., 2005





##########################################################################################################################################################
Code to asses the data:
##########################################################################################################################################################
#!/usr/bin/env python
# coding: utf-8

# In[40]:


#import tools
import pandas as pd
import numpy as np
import sys
import os
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
current_folder = os.getcwd()


# In[68]:


#get data
file_path = r"C:\Users\chris\Desktop\School\Computational Sciences\Computational Sciences Seminars\CS_Assignment-master".replace('\\','/')
data = pd.read_csv(file_path + "/istherecorrelation.csv", sep = ";")
data['WO [x1000]'] = data['WO [x1000]'].str.replace(",",".")
data['WO [x1000]'] = pd.to_numeric(data['WO [x1000]'])


# In[69]:


#have a look at the data
print(data)


# In[73]:


#create the regression model
consumptionWO = np.array(data['WO [x1000]']).reshape(-1,1)
consumptionBeer = np.array(data['NL Beer consumption [x1000 hectoliter]'])

model = LinearRegression().fit(consumptionWO, consumptionBeer)
print(f'The R-square value is: {model.score(consumptionWO, consumptionBeer)}')
print('This value is quite low and does not show a high correlation')
list_consumptionWO = [float(str(consumptionWO[i]).replace("[","").replace("]","")) for i in range(len(consumptionWO))] #change data type


# In[74]:


plt.plot(consumptionWO, consumptionBeer)
plt.plot(consumptionWO, model.predict(consumptionWO))
plt.xlabel("WO Consumption")
plt.ylabel("Beer Consumption")
plt.fill_between(list_consumptionWO, consumptionBeer,model.predict(consumptionWO), color = "grey")
plt.legend(['Data','Predicted Data'])


# In[ ]:





# In[ ]:





# In[ ]:




##########################################################################################################################################################
Code Ended
##########################################################################################################################################################

