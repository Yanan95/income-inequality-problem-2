# income inequality
Use exploratory data analysis to determine if the gap between Africa/Latin America/Asia and Europe/NorthAmerica has increased, decreased or stayed the same during the last two decades.

## problem 2a  
Using the list of countries by continent from World Atlas data, load in the countries.csv file into a pandas DataFrame and name this data set as countries. 

## correct solution  
### 这次直接从网页版导入csv  
需要利用的安装包是requests(获取网址里面的csv), 利用StringIO来转化缓存为字符串，然后用pd.read_csv()读取即可。  
> import requests  
import StringIO  
url = 'https://raw.githubusercontent.com/cs109/2014_data/master/countries.csv'  
r = requests.get(url).content  
s = StringIO.StringIO(r)
countries = pd.read_csv(s)  
countries.head()  
### 这次直接从网页版导入xls
> new_url = 'https://spreadsheets.google.com/pub?key=phAwcNAVuyj1jiMAkmq1iMg&output=xls'  
new_r = requests.get(new_url).content  
new_s = StringIO.StringIO(new_r)  
income = pd.read_excel(new_s, sheetname ='income data')  
income.head()  

⚠️ 可以直接用read_excel来读取excel格式  

## problem 2a  
Transform the data set to have years as the rows and countries as the columns. show the head  
## correct solution  
⚠️现在需要将行列互换，需要注意的是index不是columns[0],columns[0]是指index旁边那一列  
因为采用了pd.read的写法，所以现在的index是0，1，2等数字，国家在‘正式格式’中的第一列（0，1，2在indexd的位置，但是索引的时候不能索引到这一列，所以columns[0]是指的index旁边的第一列，现在需要替换掉0，1，2这个index）  
所以将第一列columns放在index的位置  
> income.index = income[income.columns[0]]  

⚠️ 记住这种用法，df.index, df.columns和其索引，income.columns[0]以及如何选中这个索引income[income.columns[0]]
现在index就变成了国家名字，但是列表的第一列还是原来的国家名字，所以需要去掉这一列  
> income = income.drop(income.columns[0]，axis=1)



⚠️
