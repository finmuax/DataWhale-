```python
import pandas as pd
import numpy as np
```

## 2.3.2 读取文件
### 2.3.2.1读取文件的拓展知识
* pandas读取数据时相对路径载入报错时，尝试使用os.getcwd()查看当前工作目录。
* TSV与CSV的区别：
  * 从名称上即可知道，TSV是用制表符（Tab,'\t'）作为字段值的分隔符；CSV是用半角逗号（','）作为字段值的分隔符；
  * Python对TSV文件的支持： Python的csv模块准确的讲应该叫做dsv模块，因为它实际上是支持范式的分隔符分隔值文件（DSV，delimiter-         * separated values）的。 delimiter参数值默认为半角逗号，即默认将被处理文件视为CSV。当delimiter='\t'时，被处理文件就是TSV。
* 读取文件的部分（适用于文件特别大的场景）
  * 通过nrows参数，来设置读取文件的前多少行，nrows是一个大于等于0的整数。
  * 分块读取


```python
data_train = pd.read_csv('./数据/train.csv')
data_test = pd.read_csv('./数据/testA.csv')
data_train_sample = pd.read_csv("./数据/train.csv",nrows=5)
```


```python
data_train.shape  # 查看数据框几行几列
data_train.columns # 查看数据框的所有列名
```




    Index(['id', 'loanAmnt', 'term', 'interestRate', 'installment', 'grade',
           'subGrade', 'employmentTitle', 'employmentLength', 'homeOwnership',
           'annualIncome', 'verificationStatus', 'issueDate', 'isDefault',
           'purpose', 'postCode', 'regionCode', 'dti', 'delinquency_2years',
           'ficoRangeLow', 'ficoRangeHigh', 'openAcc', 'pubRec',
           'pubRecBankruptcies', 'revolBal', 'revolUtil', 'totalAcc',
           'initialListStatus', 'applicationType', 'earliesCreditLine', 'title',
           'policyCode', 'n0', 'n1', 'n2', 'n3', 'n4', 'n5', 'n6', 'n7', 'n8',
           'n9', 'n10', 'n11', 'n12', 'n13', 'n14'],
          dtype='object')




```python
data_train_sample
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
      <th>id</th>
      <th>loanAmnt</th>
      <th>term</th>
      <th>interestRate</th>
      <th>installment</th>
      <th>grade</th>
      <th>subGrade</th>
      <th>employmentTitle</th>
      <th>employmentLength</th>
      <th>homeOwnership</th>
      <th>...</th>
      <th>n5</th>
      <th>n6</th>
      <th>n7</th>
      <th>n8</th>
      <th>n9</th>
      <th>n10</th>
      <th>n11</th>
      <th>n12</th>
      <th>n13</th>
      <th>n14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>35000.0</td>
      <td>5</td>
      <td>19.52</td>
      <td>917.97</td>
      <td>E</td>
      <td>E2</td>
      <td>320.0</td>
      <td>2 years</td>
      <td>2</td>
      <td>...</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>12.0</td>
      <td>2.0</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>18000.0</td>
      <td>5</td>
      <td>18.49</td>
      <td>461.90</td>
      <td>D</td>
      <td>D2</td>
      <td>219843.0</td>
      <td>5 years</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>12000.0</td>
      <td>5</td>
      <td>16.99</td>
      <td>298.17</td>
      <td>D</td>
      <td>D3</td>
      <td>31698.0</td>
      <td>8 years</td>
      <td>0</td>
      <td>...</td>
      <td>0.0</td>
      <td>21.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>11.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>11000.0</td>
      <td>3</td>
      <td>7.26</td>
      <td>340.96</td>
      <td>A</td>
      <td>A4</td>
      <td>46854.0</td>
      <td>10+ years</td>
      <td>1</td>
      <td>...</td>
      <td>16.0</td>
      <td>4.0</td>
      <td>7.0</td>
      <td>21.0</td>
      <td>6.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>3000.0</td>
      <td>3</td>
      <td>12.99</td>
      <td>101.07</td>
      <td>C</td>
      <td>C2</td>
      <td>54.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>...</td>
      <td>4.0</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>15.0</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 47 columns</p>
</div>



### 给出所有类名对应的含义
- id 为贷款清单分配的唯一信用证标识
- loanAmnt 贷款金额
- term 贷款期限（year）
- interestRate 贷款利率
- installment 分期付款金额
- grade 贷款等级
- subGrade 贷款等级之子级
- employmentTitle 就业职称
- employmentLength 就业年限（年）
- homeOwnership 借款人在登记时提供的房屋所有权状况
- annualIncome 年收入
- verificationStatus 验证状态
- issueDate 贷款发放的月份
- purpose 借款人在贷款申请时的贷款用途类别
- postCode 借款人在贷款申请中提供的邮政编码的前3位数字
- regionCode 地区编码
- dti 债务收入比
- delinquency_2years 借款人过去2年信用档案中逾期30天以上的违约事件数
- ficoRangeLow 借款人在贷款发放时的fico所属的下限范围
- ficoRangeHigh 借款人在贷款发放时的fico所属的上限范围
- openAcc 借款人信用档案中未结信用额度的数量
- pubRec 贬损公共记录的数量
- pubRecBankruptcies 公开记录清除的数量
- revolBal 信贷周转余额合计
- revolUtil 循环额度利用率，或借款人使用的相对于所有可用循环信贷的信贷金额
- totalAcc 借款人信用档案中当前的信用额度总数
- initialListStatus 贷款的初始列表状态
- applicationType 表明贷款是个人申请还是与两个共同借款人的联合申请
- earliesCreditLine 借款人最早报告的信用额度开立的月份
- title 借款人提供的贷款名称
- policyCode 公开可用的策略_代码=1新产品不公开可用的策略_代码=2
- n系列匿名特征 匿名特征n0-n14，为一些贷款人行为计数特征的处理


```python
data_train.info() # 通过info()来熟悉每一列之下是什么数据类型
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 800000 entries, 0 to 799999
    Data columns (total 47 columns):
     #   Column              Non-Null Count   Dtype  
    ---  ------              --------------   -----  
     0   id                  800000 non-null  int64  
     1   loanAmnt            800000 non-null  float64
     2   term                800000 non-null  int64  
     3   interestRate        800000 non-null  float64
     4   installment         800000 non-null  float64
     5   grade               800000 non-null  object 
     6   subGrade            800000 non-null  object 
     7   employmentTitle     799999 non-null  float64
     8   employmentLength    753201 non-null  object 
     9   homeOwnership       800000 non-null  int64  
     10  annualIncome        800000 non-null  float64
     11  verificationStatus  800000 non-null  int64  
     12  issueDate           800000 non-null  object 
     13  isDefault           800000 non-null  int64  
     14  purpose             800000 non-null  int64  
     15  postCode            799999 non-null  float64
     16  regionCode          800000 non-null  int64  
     17  dti                 799761 non-null  float64
     18  delinquency_2years  800000 non-null  float64
     19  ficoRangeLow        800000 non-null  float64
     20  ficoRangeHigh       800000 non-null  float64
     21  openAcc             800000 non-null  float64
     22  pubRec              800000 non-null  float64
     23  pubRecBankruptcies  799595 non-null  float64
     24  revolBal            800000 non-null  float64
     25  revolUtil           799469 non-null  float64
     26  totalAcc            800000 non-null  float64
     27  initialListStatus   800000 non-null  int64  
     28  applicationType     800000 non-null  int64  
     29  earliesCreditLine   800000 non-null  object 
     30  title               799999 non-null  float64
     31  policyCode          800000 non-null  float64
     32  n0                  759730 non-null  float64
     33  n1                  759730 non-null  float64
     34  n2                  759730 non-null  float64
     35  n3                  759730 non-null  float64
     36  n4                  766761 non-null  float64
     37  n5                  759730 non-null  float64
     38  n6                  759730 non-null  float64
     39  n7                  759730 non-null  float64
     40  n8                  759729 non-null  float64
     41  n9                  759730 non-null  float64
     42  n10                 766761 non-null  float64
     43  n11                 730248 non-null  float64
     44  n12                 759730 non-null  float64
     45  n13                 759730 non-null  float64
     46  n14                 759730 non-null  float64
    dtypes: float64(33), int64(9), object(5)
    memory usage: 286.9+ MB



```python
data_train.describe()# 总体粗略的查看数据集各个特征的一些基本统计量（多少个，平均值等）
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
      <th>id</th>
      <th>loanAmnt</th>
      <th>term</th>
      <th>interestRate</th>
      <th>installment</th>
      <th>employmentTitle</th>
      <th>homeOwnership</th>
      <th>annualIncome</th>
      <th>verificationStatus</th>
      <th>isDefault</th>
      <th>...</th>
      <th>n5</th>
      <th>n6</th>
      <th>n7</th>
      <th>n8</th>
      <th>n9</th>
      <th>n10</th>
      <th>n11</th>
      <th>n12</th>
      <th>n13</th>
      <th>n14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>800000.000000</td>
      <td>800000.000000</td>
      <td>800000.000000</td>
      <td>800000.000000</td>
      <td>800000.000000</td>
      <td>799999.000000</td>
      <td>800000.000000</td>
      <td>8.000000e+05</td>
      <td>800000.000000</td>
      <td>800000.000000</td>
      <td>...</td>
      <td>759730.000000</td>
      <td>759730.000000</td>
      <td>759730.000000</td>
      <td>759729.000000</td>
      <td>759730.000000</td>
      <td>766761.000000</td>
      <td>730248.000000</td>
      <td>759730.000000</td>
      <td>759730.000000</td>
      <td>759730.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>399999.500000</td>
      <td>14416.818875</td>
      <td>3.482745</td>
      <td>13.238391</td>
      <td>437.947723</td>
      <td>72005.351714</td>
      <td>0.614213</td>
      <td>7.613391e+04</td>
      <td>1.009683</td>
      <td>0.199513</td>
      <td>...</td>
      <td>8.107937</td>
      <td>8.575994</td>
      <td>8.282953</td>
      <td>14.622488</td>
      <td>5.592345</td>
      <td>11.643896</td>
      <td>0.000815</td>
      <td>0.003384</td>
      <td>0.089366</td>
      <td>2.178606</td>
    </tr>
    <tr>
      <th>std</th>
      <td>230940.252015</td>
      <td>8716.086178</td>
      <td>0.855832</td>
      <td>4.765757</td>
      <td>261.460393</td>
      <td>106585.640204</td>
      <td>0.675749</td>
      <td>6.894751e+04</td>
      <td>0.782716</td>
      <td>0.399634</td>
      <td>...</td>
      <td>4.799210</td>
      <td>7.400536</td>
      <td>4.561689</td>
      <td>8.124610</td>
      <td>3.216184</td>
      <td>5.484104</td>
      <td>0.030075</td>
      <td>0.062041</td>
      <td>0.509069</td>
      <td>1.844377</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>500.000000</td>
      <td>3.000000</td>
      <td>5.310000</td>
      <td>15.690000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>199999.750000</td>
      <td>8000.000000</td>
      <td>3.000000</td>
      <td>9.750000</td>
      <td>248.450000</td>
      <td>427.000000</td>
      <td>0.000000</td>
      <td>4.560000e+04</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>5.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>9.000000</td>
      <td>3.000000</td>
      <td>8.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>399999.500000</td>
      <td>12000.000000</td>
      <td>3.000000</td>
      <td>12.740000</td>
      <td>375.135000</td>
      <td>7755.000000</td>
      <td>1.000000</td>
      <td>6.500000e+04</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>13.000000</td>
      <td>5.000000</td>
      <td>11.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>599999.250000</td>
      <td>20000.000000</td>
      <td>3.000000</td>
      <td>15.990000</td>
      <td>580.710000</td>
      <td>117663.500000</td>
      <td>1.000000</td>
      <td>9.000000e+04</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>10.000000</td>
      <td>19.000000</td>
      <td>7.000000</td>
      <td>14.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>799999.000000</td>
      <td>40000.000000</td>
      <td>5.000000</td>
      <td>30.990000</td>
      <td>1715.420000</td>
      <td>378351.000000</td>
      <td>5.000000</td>
      <td>1.099920e+07</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>...</td>
      <td>70.000000</td>
      <td>132.000000</td>
      <td>79.000000</td>
      <td>128.000000</td>
      <td>45.000000</td>
      <td>82.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>39.000000</td>
      <td>30.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 42 columns</p>
</div>




```python
data_train.head(3).append(data_train.tail(3)) # 查看前三行和后三行
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
      <th>id</th>
      <th>loanAmnt</th>
      <th>term</th>
      <th>interestRate</th>
      <th>installment</th>
      <th>grade</th>
      <th>subGrade</th>
      <th>employmentTitle</th>
      <th>employmentLength</th>
      <th>homeOwnership</th>
      <th>...</th>
      <th>n5</th>
      <th>n6</th>
      <th>n7</th>
      <th>n8</th>
      <th>n9</th>
      <th>n10</th>
      <th>n11</th>
      <th>n12</th>
      <th>n13</th>
      <th>n14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>35000.0</td>
      <td>5</td>
      <td>19.52</td>
      <td>917.97</td>
      <td>E</td>
      <td>E2</td>
      <td>320.0</td>
      <td>2 years</td>
      <td>2</td>
      <td>...</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>12.0</td>
      <td>2.0</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>18000.0</td>
      <td>5</td>
      <td>18.49</td>
      <td>461.90</td>
      <td>D</td>
      <td>D2</td>
      <td>219843.0</td>
      <td>5 years</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>12000.0</td>
      <td>5</td>
      <td>16.99</td>
      <td>298.17</td>
      <td>D</td>
      <td>D3</td>
      <td>31698.0</td>
      <td>8 years</td>
      <td>0</td>
      <td>...</td>
      <td>0.0</td>
      <td>21.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>11.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>799997</th>
      <td>799997</td>
      <td>6000.0</td>
      <td>3</td>
      <td>13.33</td>
      <td>203.12</td>
      <td>C</td>
      <td>C3</td>
      <td>2582.0</td>
      <td>10+ years</td>
      <td>1</td>
      <td>...</td>
      <td>4.0</td>
      <td>26.0</td>
      <td>4.0</td>
      <td>10.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>799998</th>
      <td>799998</td>
      <td>19200.0</td>
      <td>3</td>
      <td>6.92</td>
      <td>592.14</td>
      <td>A</td>
      <td>A4</td>
      <td>151.0</td>
      <td>10+ years</td>
      <td>0</td>
      <td>...</td>
      <td>10.0</td>
      <td>6.0</td>
      <td>12.0</td>
      <td>22.0</td>
      <td>8.0</td>
      <td>16.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>799999</th>
      <td>799999</td>
      <td>9000.0</td>
      <td>3</td>
      <td>11.06</td>
      <td>294.91</td>
      <td>B</td>
      <td>B3</td>
      <td>13.0</td>
      <td>5 years</td>
      <td>0</td>
      <td>...</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
<p>6 rows × 47 columns</p>
</div>



## 2.3.4查看数据集中特征缺失值，唯一值等


```python
# 查看缺失值
print(f'There are {data_train.isnull().any().sum()} columns in train dataset with missing values.')
```

    There are 22 columns in train dataset with missing values.



```python
# 上面得到训练集有22列特征有缺失值，进一步查看缺失特征中缺失率大于1%的特征
have_null_fea_dict = (data_train.isnull().sum()/len(data_train)).to_dict()
fea_null_moreThanHalf = {}
for key,value in have_null_fea_dict.items():
    if value > 0.01:
        fea_null_moreThanHalf[key] = value
        
fea_null_moreThanHalf
```




    {'employmentLength': 0.05849875,
     'n0': 0.0503375,
     'n1': 0.0503375,
     'n2': 0.0503375,
     'n3': 0.0503375,
     'n4': 0.04154875,
     'n5': 0.0503375,
     'n6': 0.0503375,
     'n7': 0.0503375,
     'n8': 0.05033875,
     'n9': 0.0503375,
     'n10': 0.04154875,
     'n11': 0.08719,
     'n12': 0.0503375,
     'n13': 0.0503375,
     'n14': 0.0503375}



- 纵向了解哪些列存在 “nan”, 并可以把nan的个数打印，主要的目的在于查看某一列nan存在的个数是否真的很大，如果nan存在的过多，说明这一列对label的影响几乎不起作用了，可以考虑删掉。如果缺失值很小一般可以选择填充。
- 另外可以横向比较，如果在数据集中，某些样本数据的大部分列都是缺失的且样本足够的情况下可以考虑删除

Tips: 比赛大杀器lgb模型可以自动处理缺失值，Task4模型会具体学习模型了解模型哦！


```python
# 具体的查看缺失特征及缺失率
# 可视化
missing = data_train.isnull().sum()/len(data_train)
missing = missing[missing > 0]
missing.sort_values(inplace=True)
missing.plot.bar()
```

               id  loanAmnt   term  interestRate  installment  grade  subGrade  \
    0       False     False  False         False        False  False     False   
    1       False     False  False         False        False  False     False   
    2       False     False  False         False        False  False     False   
    3       False     False  False         False        False  False     False   
    4       False     False  False         False        False  False     False   
    ...       ...       ...    ...           ...          ...    ...       ...   
    799995  False     False  False         False        False  False     False   
    799996  False     False  False         False        False  False     False   
    799997  False     False  False         False        False  False     False   
    799998  False     False  False         False        False  False     False   
    799999  False     False  False         False        False  False     False   
    
            employmentTitle  employmentLength  homeOwnership  ...     n5     n6  \
    0                 False             False          False  ...  False  False   
    1                 False             False          False  ...   True   True   
    2                 False             False          False  ...  False  False   
    3                 False             False          False  ...  False  False   
    4                 False              True          False  ...  False  False   
    ...                 ...               ...            ...  ...    ...    ...   
    799995            False             False          False  ...  False  False   
    799996            False             False          False  ...  False  False   
    799997            False             False          False  ...  False  False   
    799998            False             False          False  ...  False  False   
    799999            False             False          False  ...  False  False   
    
               n7     n8     n9    n10    n11    n12    n13    n14  
    0       False  False  False  False  False  False  False  False  
    1        True   True   True  False   True   True   True   True  
    2       False  False  False  False  False  False  False  False  
    3       False  False  False  False  False  False  False  False  
    4       False  False  False  False  False  False  False  False  
    ...       ...    ...    ...    ...    ...    ...    ...    ...  
    799995  False  False  False  False  False  False  False  False  
    799996  False  False  False  False  False  False  False  False  
    799997  False  False  False  False  False  False  False  False  
    799998  False  False  False  False  False  False  False  False  
    799999  False  False  False  False  False  False  False  False  
    
    [800000 rows x 47 columns]





    <matplotlib.axes._subplots.AxesSubplot at 0x7fe706c04700>




![png](output_13_2.png)



```python
# 查看训练集测试集中特征属性只有一值的特征
one_value_fea = [col for col in data_train.columns if data_train[col].nunique() <= 1]
one_value_fea_test = [col for col in data_test.columns if data_test[col].nunique() <= 1]

print(f'There are {len(one_value_fea)} columns in train dataset with one unique value.')
print(f'There are {len(one_value_fea_test)} columns in test dataset with one unique value.')
```

    There are 1 columns in train dataset with one unique value.
    There are 1 columns in test dataset with one unique value.


### 总结：
47列数据中有22列都缺少数据，这在现实世界中很正常。‘policyCode’具有一个唯一值（或全部缺失）。有很多连续变量和一些分类变量。

## 2.3.5 查看特征的数值类型有哪些，对象类型有哪些
> [什么是数值类型和对象类型](http://www.datasoldier.net/archives/878')

* 特征一般都是由***类别型特征***和***数值型特征***组成，而数值型特征又分为连续型和离散型。
* 类别型特征有时具有非数值关系，有时也具有数值关系。比如‘grade’中的等级A，B，C等，是否只是单纯的分类，还是A优于其他要结合业务判断。
* 数值型特征本是可以直接入模的，但往往风控人员要对其做分箱，转化为WOE编码进而做标准评分卡等操作。从模型效果上来看，特征分箱主要是为了降低变量的复杂性，减少变量噪音对模型的影响，提高自变量和因变量的相关度。从而使模型更加稳定


```python
numerical_fea = list(data_train.select_dtypes(exclude=['object']).columns)
category_fea = list(filter(lambda x: x not in numerical_fea,list(data_train.columns)))
```


```python
numerical_fea
```




    ['id',
     'loanAmnt',
     'term',
     'interestRate',
     'installment',
     'employmentTitle',
     'homeOwnership',
     'annualIncome',
     'verificationStatus',
     'isDefault',
     'purpose',
     'postCode',
     'regionCode',
     'dti',
     'delinquency_2years',
     'ficoRangeLow',
     'ficoRangeHigh',
     'openAcc',
     'pubRec',
     'pubRecBankruptcies',
     'revolBal',
     'revolUtil',
     'totalAcc',
     'initialListStatus',
     'applicationType',
     'title',
     'policyCode',
     'n0',
     'n1',
     'n2',
     'n3',
     'n4',
     'n5',
     'n6',
     'n7',
     'n8',
     'n9',
     'n10',
     'n11',
     'n12',
     'n13',
     'n14']




```python
data_train['grade']
```




    0         E
    1         D
    2         D
    3         A
    4         C
             ..
    799995    C
    799996    A
    799997    C
    799998    A
    799999    B
    Name: grade, Length: 800000, dtype: object



### 数值型变量分析，数值型肯定是包括连续型变量和离散型变量的，找出来
划分数值型变量中的连续变量和离散型变量



```python
#过滤数值型类别特征
def get_numerical_serial_fea(data,feas):
    numerical_serial_fea = []
    numerical_noserial_fea = []
    for fea in feas:
        temp = data[fea].nunique()
        if temp <= 10:
            numerical_noserial_fea.append(fea)
            continue
        numerical_serial_fea.append(fea)
    return numerical_serial_fea,numerical_noserial_fea

numerical_serial_fea,numerical_noserial_fea = get_numerical_serial_fea(data_train,numerical_fea)
```

* 数值类别型变量分析



```python
data_train['term'].value_counts()#统计’term‘列中 每个离散型变量的数量
```




    3    606902
    5    193098
    Name: term, dtype: int64




```python
data_train['homeOwnership'].value_counts()
data_train['verificationStatus'].value_counts()
data_train['initialListStatus'].value_counts()
data_train['applicationType'].value_counts()
data_train['policyCode'].value_counts()#离散型变量，无用，全部一个值
data_train['n11'].value_counts()#离散型变量，相差悬殊，用不用再分析
data_train['n12'].value_counts()#离散型变量，相差悬殊，用不用再分析
```




    0.0    757315
    1.0      2281
    2.0       115
    3.0        16
    4.0         3
    Name: n12, dtype: int64



* 数值连续型变量分析
