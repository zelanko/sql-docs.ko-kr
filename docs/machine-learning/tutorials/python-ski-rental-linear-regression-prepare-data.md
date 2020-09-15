---
title: 'Python 자습서: 데이터 준비'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 2부에서는 R을 통해 데이터를 준비하여 SQL 기계 학습에서 스키 대여 수요를 예측합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 07b2cf5a77199f64d89d8dd61f8ec89268d759c5
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173412"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-with-sql-machine-learning"></a>Python 자습서: SQL 기계 학습을 사용하여 선형 회귀 모델을 학습시킬 데이터 준비
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서 이 데이터를 사용하여 SQL Server Machine Learning Services 또는 빅 데이터 클러스터에서 Python으로 선형 회귀 모델을 학습시키고 배포할 것입니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서 이 데이터를 사용하여 SQL Server Machine Learning Services를 통해 Python에서 선형 회귀 모델을 학습하고 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 후반부에서 이 데이터를 사용하여 Azure SQL Managed Instance Machine Learning Services를 통해 Python에서 선형 회귀 모델을 학습시키고 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 데이터베이스의 데이터를 **pandas** 데이터 프레임에 로드
> * 일부 열을 제거하여 Python에서 데이터 준비

[1부](python-ski-rental-linear-regression.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[3부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 기계 학습 모델을 학습하는 방법을 알아봅니다.

[4부](python-ski-rental-linear-regression-deploy-model.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 2부에서는 [1부](python-ski-rental-linear-regression.md)와 해당 필수 구성 요소를 완료했다고 가정합니다.

## <a name="explore-and-prepare-the-data"></a>데이터 탐색 및 준비

Python에서 데이터를 사용하려면 데이터베이스에서 pandas 데이터 프레임으로 데이터를 로드합니다.

Azure Data Studio에서 새 Python Notebook을 만들고 아래 스크립트를 실행합니다. 

아래 Python 스크립트는 데이터베이스의 **dbo.rental_data** 테이블에서 pandas 데이터 프레임 **df**로 데이터 세트를 가져옵니다.

연결 문자열에서 필요에 따라 연결 세부 정보를 바꿉니다.

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<server>; DATABASE=TutorialDB;UID=<username>;PWD=<password>)

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

다음과 비슷한 결과가 표시됩니다.

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 2부에서 다음 단계를 완료했습니다.

* 데이터베이스의 데이터를 **pandas** 데이터 프레임에 로드
* 일부 열을 제거하여 Python에서 데이터 준비

TutorialDB 데이터베이스의 데이터를 사용하는 기계 학습 모델을 학습하려면 다음 자습서 시리즈의 3부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델 학습](python-ski-rental-linear-regression-train-model.md)