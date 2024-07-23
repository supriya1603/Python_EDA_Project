# Python_EDA_Project
#!/usr/bin/env python
# coding: utf-8

# In[3]:


import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
get_ipython().run_line_magic('matplotlib', 'inline')
import seaborn as sns


# In[4]:


df = pd.read_csv('C:\\Users\\kushw\\Downloads\\Diwali Sales Data.csv', encoding='unicode_escape')


# In[5]:


df.shape


# In[6]:


df.head(10)


# In[7]:


df.info()


# In[8]:


df.drop(['Status','unnamed1'],axis=1,inplace=True)


# In[9]:


pd.isnull(df)


# In[10]:


pd.isnull(df).sum()


# In[12]:


df.shape


# In[13]:


df.dropna(inplace=True)


# In[14]:


df.shape


# In[15]:


pd.isnull(df).sum()


# In[16]:


df['Amount'] = df['Amount'].astype('int')


# In[17]:


df['Amount'].dtypes


# In[18]:


df.columns


# In[19]:


df.rename(columns={'Marital_Status':'Shaadi'})


# In[20]:


df.describe()


# In[21]:


df[['Age','Orders','Amount']].describe()


# # Exploratory Data Analysis
# 

# ## Gender

# In[26]:


df.columns


# In[29]:


ax = sns.countplot(x = 'Gender', data = df)
for bars in ax.containers:
    ax.bar_label(bars)


# In[32]:


sales_gen = df.groupby(['Gender'],as_index = False)['Amount'].sum().sort_values(by='Amount', ascending = False)
sns.barplot(x='Gender', y='Amount', data = sales_gen)


# #### Insights from the data : Most of the buyers are female and even the purchasing power of females are greater than men

# ## Age

# In[33]:


df.columns


# In[36]:


ax = sns.countplot(data=df, x = 'Age Group', hue = 'Gender')
for bar in ax.containers:
    ax.bar_label(bar)


# In[39]:


sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending = False)

sns.barplot(x = 'Age Group', y='Amount', data = sales_age)


# #### Insights from the data : Most of the buyers are of the age group between 26-35 years female

# ## State

# In[42]:


df.columns


# In[47]:


sales_state = df.groupby(['State'], as_index = False)['Orders'].sum().sort_values(by='Orders', ascending = False).head(10)
sns.set(rc = {'figure.figsize':(17,5)})
sns.barplot(data = sales_state, x = 'State', y='Orders')


# In[48]:


sales_state = df.groupby(['State'], as_index = False)['Amount'].sum().sort_values(by='Amount', ascending = False).head(10)
sns.set(rc = {'figure.figsize':(17,5)})
sns.barplot(data = sales_state, x = 'State', y='Amount')


# #### Insights from the data : Most of the orders & total sales/amount are from Uttar Pradesh, Maharashtra & Karnataka.

# ## Marital Status

# In[49]:


ax = sns.countplot(data = df, x = 'Marital_Status')

sns.set(rc={'figure.figsize':(8,5)})
for bars in ax.containers:
    ax.bar_label(bars)


# In[50]:


sales_state = df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

sns.set(rc={'figure.figsize':(6,5)})
sns.barplot(data = sales_state, x = 'Marital_Status',y= 'Amount', hue='Gender')


# #### Insights from the data : Most of the buyers are married (women) & they have high purchasing power.

# ## Occupation

# In[53]:


sns.set(rc={'figure.figsize':(19,5)})
ax = sns.countplot(data = df, x = 'Occupation')

for bars in ax.containers:
    ax.bar_label(bars)


# In[54]:


sales_state = df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

sns.set(rc={'figure.figsize':(19,5)})
sns.barplot(data = sales_state, x = 'Occupation',y= 'Amount')


# #### Insights from the data : Most of the buyers are working in the IT Sector, Aviation & Healthcare.

# ## Product Category

# In[63]:


df.columns


# In[70]:


product = df.groupby(['Product_Category'], as_index = False)['Orders'].sum().sort_values(by='Orders', ascending = False).head(10)
sns.set(rc = {'figure.figsize':(19,5)})
sns.barplot(data = product, x = 'Product_Category', y='Orders')


# In[68]:


fig1, ax1 = plt.subplots(figsize=(12,7))
df.groupby('Product_ID')['Orders'].sum().nlargest(10).sort_values(ascending=False).plot(kind='bar')


# ## Conclusion 

# #### 
# - Married women age group 26-35 years from Uttar Pradesh, Maharastra and Karnataka working in IT, Healthcare and Aviation are more likely to buy products from Food, Clothing and Electronics category.
