---
title: 'Python 자습서: 데이터 준비'
description: 4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 통해 데이터를 준비하여 SQL Server Machine Learning Services에서 스키 대여 정보를 예측합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9aeefb0b6fd9ca1a744d132fccf1eedfedbaa6e7
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116426"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 자습서: SQL Server Machine Learning Services에서 선형 회귀 모델을 학습하기 위한 데이터 준비
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 4부 자습서 시리즈의 2부에서는 Python을 사용하여 SQL Server 데이터베이스에서 데이터를 준비합니다. 이 시리즈의 뒷부분에서 이 데이터를 사용하여 SQL Server Machine Learning Services를 통해 Python에서 선형 회귀 모델을 학습하고 배포합니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

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

연결 문자열에서 필요에 따라 연결 세부 정보를 바꿉니다.

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=TutorialDB; Trusted_Connection=yes')

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

* SQL Server 데이터베이스에서 **pandas** 데이터 프레임으로 데이터 로드
* 일부 열을 제거하여 Python에서 데이터 준비

TutorialDB 데이터베이스의 데이터를 사용하는 기계 학습 모델을 학습하려면 다음 자습서 시리즈의 3부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델 학습](python-ski-rental-linear-regression-train-model.md)