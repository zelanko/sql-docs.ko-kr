---
title: 'Python 자습서: 데이터 준비'
description: 이 자습서에서는 SQL Server Machine Learning Services에서 Python 및 선형 회귀를 사용하여 스키 대여 수를 예측합니다. Python을 사용하여 SQL Server 데이터베이스에서 데이터를 준비합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6424a453bff2f0f6d62caa8c9870ccc2ec10d578
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727060"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 자습서: SQL Server Machine Learning Services에서 선형 회귀 모델을 학습하기 위한 데이터 준비
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 4부 자습서 시리즈의 2부에서는 Python을 사용하여 SQL Server 데이터베이스에서 데이터를 준비합니다. 이 시리즈의 뒷부분에서 이 데이터를 사용하여 SQL Server Machine Learning Services를 통해 Python에서 선형 회귀 모델을 학습하고 배포합니다.

이 문서에서는 다음과 같은 방법을 알아봅니다.

> [!div class="checklist"]
> * SQL Server 데이터베이스에서 **pandas** 데이터 프레임으로 데이터 로드
> * 일부 열을 제거하여 Python에서 데이터 준비

[1부](python-ski-rental-linear-regression.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[3부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 기계 학습 모델을 학습하는 방법을 알아봅니다.

[4부](python-ski-rental-linear-regression-deploy-model.md)에서는 모델을 SQL Server에 저장하는 방법을 알아본 다음, 2부와 3부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 새 데이터를 기반으로 예측하기 위해 SQL Server에서 실행됩니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 2부에서는 [1부](python-ski-rental-linear-regression.md)와 해당 필수 구성 요소를 완료했다고 가정합니다.

## <a name="explore-and-prepare-the-data"></a>데이터 탐색 및 준비

Python에서 데이터를 사용하려면 SQL Server 데이터베이스에서 pandas 데이터 프레임으로 데이터를 로드합니다.

Azure Data Studio에서 새 Python Notebook을 만들고 다음 스크립트를 실행합니다. `<SQL Server>`를 사용자 고유의 SQL Server 이름으로 바꿉니다.

아래 Python 스크립트는 데이터베이스의 **dbo.rental_data** 테이블에서 pandas 데이터 프레임 **df**로 데이터 세트를 가져옵니다.

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

다음과 비슷한 결과가 표시됩니다.

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

이 자습서 시리즈의 2부에서 다음 단계를 완료했습니다.

* SQL Server 데이터베이스에서 **pandas** 데이터 프레임으로 데이터 로드
* 일부 열을 제거하여 Python에서 데이터 준비

TutorialDB 데이터베이스의 데이터를 사용하는 기계 학습 모델을 학습하려면 다음 자습서 시리즈의 3부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델 학습](python-ski-rental-linear-regression-train-model.md)