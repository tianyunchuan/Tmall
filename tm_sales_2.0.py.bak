# -*- coding: utf-8 -*-
"""
Created on Thu Feb  1 19:26:28 2018

@author: tianyunchuan
"""
import MySQLdb
import numpy as np
import numpy
import pandas as pd
import pandas
import re
import datetime
import time
import os
from pandas import Series,DataFrame
import matplotlib
from matplotlib import pyplot as plt
from pandas import read_csv
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
from pandas.tools.plotting import scatter_matrix
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn import neighbors
from sklearn.model_selection import cross_val_score
from sklearn.naive_bayes import BernoulliNB
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import cross_val_score
import urllib.request
import urllib.parse
import urllib.error
from pprint import pprint
import http.cookiejar
import http.cookiejar as cookielib;
import requests
from urllib.request import urlretrieve
from bs4 import BeautifulSoup
import seaborn as sns
import hashlib
from selenium import webdriver
from sqlalchemy import create_engine
from importlib import reload
import math
import random
import tushare as ts
import functools
import operator
from lxml import etree
import codecs
import json
from enum import Enum
from urllib import request 

headers={
    'User-Agent':'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36',
    'referer':'https://list.tmall.com/search_product.htm?spm=a220m.1000858.1000720.2.25f405efnboSzV&brand=20448&q=%C4%CC%C6%BF&sort=s&style=g&from=sn_1_brand-qp#J_crumbs',
    'cookie':r'x=__ll%3D-1%26_ato%3D0; hng=; uc1=cookie14=UoTcBzlZe54kNg%3D%3D&lng=zh_CN&cookie16=U%2BGCWk%2F74Mx5tgzv3dWpnhjPaQ%3D%3D&existShop=false&cookie21=WqG3DMC9Ed9Ujk%2B1SA%2FENQ%3D%3D&tag=10&cookie15=U%2BGCWk%2F75gdr5Q%3D%3D&pas=0; uc3=sg2=AHgGkeL5BqkKuU4YcB%2BSUeQKS%2BFxEn5S8uVz0C8eqEo%3D&nk2=F4%2B0RmK%2BEw%3D%3D&id2=VvuEK%2FTxJyw%3D&vt3=F8dBzLE2qhdlq7Qjmvw%3D&lg2=VFC%2FuZ9ayeYq2g%3D%3D; tracknick=tyc1900; ck1=; lgc=tyc1900; cookie2=65e32eeff204e4f6e49794b1d2a080e0; t=bdb9d2b63f149a1588a09de537ad7184; skt=78d450c0afa2b979; _tb_token_=f77338de5eb7b; whl=-1%260%260%260; otherx=e%3D1%26p%3D*%26s%3D0%26c%3D0%26f%3D0%26g%3D0%26t%3D0; cna=gMlrEtN2LDsCAXTpN3+A85yu; isg=AlFRjOmi7IyfNgCQePCz8l9cYF0rFsVVROyF-DPmSpg12nEsew7VAP8wCpjH'
    }  
 
url_base='https://list.tmall.com/search_product.htm?spm=875.7931836/B.subpannel2016043.22.59e64265bs0yRv&q=%B0%B2%C8%AB%D7%F9%D2%CE&pos=3&cat=50544006&end_price=9999&start_price=999&style=g&from=.list.pc_1_searchbutton&acm=2016030719.1003.2.719062&sort=s&search_condition=48&scm=1003.2.2016030719.OTHER_1457808235604_719062&brand=33467%2C3859737%2C3334835%2C3560040%2C18325119%2C33474%2C133392867%2C116455022%2C143026375%2C238314669%2C122013506%2C18351723%2C560442475'
#牛奶 https://list.tmall.com/search_product.htm?spm=a220m.1000858.1000721.2.594175b2UQlWYe&cat=50099987&q=%C5%A3%C4%CC&sort=s&style=g&from=sn_1_cat-qp&active=2#J_crumbs
htmls=requests.get(url_base,headers=headers).text
soup=BeautifulSoup(htmls,'lxml')
lastpage=re.findall(re.compile(r'共(\d+)页'),htmls)
lastpage=int(lastpage[0])
anchors_all=[]

urls=[]


time_start=datetime.datetime.now()

#lastpage=12

for i in range(0,5):
    for j in range(i,lastpage,5):
        urls=[]
        url=re.sub('&q=%','&s='+str(j*60)+'&q=%',url_base)
        urls.append(url)
  
        for url in urls:    
            htmls=requests.get(url,headers=headers).text
            soup=BeautifulSoup(htmls,'lxml')
            
            sku_blocks=soup.find_all(class_='product-iWrap')
            len(sku_blocks)
            anchors=[]
         
            for s in sku_blocks:
                title_element=s.find_all(class_='productTitle')
                price_element=s.find_all(class_='productPrice')
                shop_element=s.find_all(class_='productShop')        
                status_element=s.find_all(class_='productStatus')
                
                try:
                    title=title_element[0].get_text().strip()
                    href=title_element[0].a['href']
                    price=price_element[0].get_text().strip()
                    shop=shop_element[0].get_text().strip()       
                    status_txt=status_element[0].get_text().strip() 
                    s_qty=re.findall(r'\d+.*?笔',status_txt)[0]
                    c_qty=re.findall(r'评价 ([\s\S]*)',status_txt)[0]
                    cate=soup.title.get_text().strip('天猫Tmall.com-理想生活上天猫')
                    timer=time.strftime("%Y-%m-%d")
                    anchor={'title':title,'href':href,'price':price,'shop':shop,'s_qty':s_qty,'c_qty':c_qty,'cate':cate,'timer':timer}
                    anchors.append(anchor)
                    anchors_all.append(anchor)
                except Exception:
                    print('异常') 
        time.sleep(181)
    time.sleep(361)
time_end=datetime.datetime.now()    

       
df = pd.DataFrame(columns=['bak'])  
for key in anchors_all[0].keys():
#    df=pd.DataFrame([s[key] for s in anchors])
#    df=df.append(pd.DataFrame([s[key] for s in anchors]))
#    df = pd.concat([df, pd.DataFrame([s[key] for s in anchors])], axis=1)
    p=pd.DataFrame([s[key] for s in anchors_all])
    df[key]=[s[key] for s in anchors_all]
del df['bak']
df['skuId']=[re.findall(r'.*skuId=(\d+).*',s)[0] for s in df['href']]
            
yconnect = create_engine('mysql+mysqldb://root:Tt65212879@rm-uf675p1vvls0t85vko.mysql.rds.aliyuncs.com:3306/tm_xiaoliang?charset=utf8')

pd.io.sql.to_sql(df,'tm_xl_test', yconnect, schema='tm_xiaoliang', if_exists='append',index=False)

pd.io.sql.to_sql(df,'tm_xl_bbcar', yconnect, schema='tm_xiaoliang', if_exists='append',index=False)

pd.io.sql.to_sql(df,'tm_xl_childseat', yconnect, schema='tm_xiaoliang', if_exists='append',index=False)

pd.io.sql.to_sql(df,'tm_xl_milk', yconnect, schema='tm_xiaoliang', if_exists='append',index=False)
    time.sleep(301)      
time_end=datetime.datetime.now()         


tt=re.findall(r'.*skuId=(\d+).*','//detail.tmall.com/item.htm?id=556307744414&skuId=3441564448243&areaId=310100&user_id=2549841410&cat_id=50544006&is_b=1&rn=60fb2f564d43d887863782dd3591d36d')[0]


type(df['href'])



#==============================================================================
# connection = MySQLdb.connect(
#     host='rm-uf675p1vvls0t85vko.mysql.rds.aliyuncs.com',
#     user='root',
#     passwd='Tt65212879',
#     port=3306,
#     db='tm_xiaoliang',
#     charset='utf8'
# );
# 
# df = pandas.read_sql(
#     """
#         SELECT * FROM tm_xl_niunai;
#     """, 
#     con=connection
# );
# 
# df['skuId']=[re.findall(r'.*skuId=(\d+).*',s)[0] for s in df['href']]
#==============================================================================
