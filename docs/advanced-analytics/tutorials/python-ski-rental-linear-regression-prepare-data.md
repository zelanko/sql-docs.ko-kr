---
title: 'Python 자습서: 데이터 준비 (선형 회귀)'
description: 이 자습서에서는 SQL Server Machine Learning Services에서 Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다. Python을 사용 하 여 SQL Server 데이터베이스에서 데이터를 준비 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242501"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 자습서: 데이터를 준비 하 여 SQL Server Machine Learning Services에서 선형 회귀 모델 학습
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

네 부분으로 구성 된 자습서 시리즈의 2 부에서는 Python을 사용 하 여 SQL Server 데이터베이스에서 데이터를 준비 합니다. 이 시리즈의 뒷부분에서이 데이터를 사용 하 여 SQL Server Machine Learning Services으로 Python에서 선형 회귀 모델을 학습 하 고 배포 합니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * SQL Server 데이터베이스에서 **pandas** 데이터 프레임으로 데이터 로드
> * 일부 열을 제거 하 여 Python에서 데이터 준비

[1 부](python-ski-rental-linear-regression.md)에서는 샘플 데이터베이스를 복원 하는 방법을 배웠습니다.

[3 부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 기계 학습 모델을 학습 하는 방법을 배웁니다.

[4 부](python-ski-rental-linear-regression-deploy-model.md)에서는 SQL Server에 모델을 저장 한 다음 2 단계와 3 부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법에 대해 알아봅니다. 저장 프로시저는 새 데이터를 기반으로 예측을 수행 하기 위해 SQL Server에서 실행 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 2 부에서는 [1 부](python-ski-rental-linear-regression.md) 및 해당 필수 구성 요소를 완료 했다고 가정 합니다.

## <a name="explore-and-prepare-the-data"></a>데이터 탐색 및 준비

Python에서 데이터를 사용 하려면 SQL Server 데이터베이스에서 pandas 데이터 프레임으로 데이터를 로드 합니다.

Azure Data Studio에서 새 Python 노트북을 만들고 다음 스크립트를 실행 합니다. 를 `<SQL Server>` 사용자 고유의 SQL Server 이름으로 바꿉니다.

아래의 Python 스크립트는 데이터베이스의 **rental_data** 테이블에서 pandas 데이터 프레임 **df**로 데이터 집합을 가져옵니다.

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

다음과 유사한 결과가 표시 됩니다.

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 2 부에서는 다음 단계를 완료 했습니다.

* SQL Server 데이터베이스에서 **pandas** 데이터 프레임으로 데이터 로드
* 일부 열을 제거 하 여 Python에서 데이터 준비

TutorialDB 데이터베이스의 데이터를 사용 하는 기계 학습 모델을 학습 하려면이 자습서 시리즈의 3 부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델 학습](python-ski-rental-linear-regression-train-model.md)