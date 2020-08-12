---
title: '자습서: R에서 예측 모델을 학습하기 위한 데이터 준비'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 2부에서는 R에서 SQL 기계 학습을 사용하여 예측 모델을 학습시키기 위한 데이터를 준비합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e0c679ce4a146065223123e41cb2935e7d33ad71
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784076"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 예측 모델을 학습시키기 위한 데이터 준비
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 R을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서는 R에서 SQL Server Machine Learning Services 또는 빅 데이터 클러스터를 사용하여 이 데이터로 예측 모델을 학습시키고 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 R을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서는 R에서 SQL Server Machine Learning Services를 사용하여 이 데이터로 예측 모델을 학습시키고 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 R을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서는 R에서 SQL Server R Services를 사용하여 이 데이터로 예측 모델을 학습시키고 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 R을 사용하여 데이터베이스의 데이터를 준비합니다. 이 시리즈의 뒷부분에서는 R에서 Azure SQL Managed Instance Machine Learning Services를 사용하여 이 데이터로 예측 모델을 학습시키고 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 샘플 데이터베이스를 데이터베이스에 복원
> * 데이터베이스의 데이터를 R 데이터 프레임에 로드
> * 일부 열을 범주로 식별하여 R에서 데이터 준비

[1부](r-predictive-model-introduction.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[3부](r-predictive-model-train.md)에서는 R에서 기계 학습 모델을 학습시키는 방법을 알아봅니다.

[4부](r-predictive-model-deploy.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 R 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서 시리즈의 2부에서는 [**1부**](r-predictive-model-introduction.md) 및 해당 전제 작업을 완료했다고 가정합니다.

## <a name="load-the-data-into-a-data-frame"></a>데이터 프레임에 데이터 로드

R에서 데이터를 사용하려면 데이터베이스의 데이터를 데이터 프레임(`rentaldata`)에 로드합니다.

RStudio에서 새 RScript 파일을 만든 후 다음 스크립트를 실행합니다. **ServerName**을 해당하는 연결 정보로 바꿉니다.

```r
#Define the connection string to connect to the TutorialDB database
connStr <- "Driver=SQL Server;Server=ServerName;Database=TutorialDB;uid=Username;pwd=Password"


#Get the data from the table
library(RODBC)

ch <- odbcDriverConnect(connStr)

#Import the data from the table
rentaldata <- sqlFetch(ch, "dbo.rental_data")

#Take a look at the structure of the data and the top rows
head(rentaldata)
str(rentaldata)
```

다음과 비슷한 결과가 표시됩니다.

```results
   Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
1  2014    1     20      445         2        1      0
2  2014    2     13       40         5        0      0
3  2013    3     10      456         1        0      0
4  2014    3     31       38         2        0      0
5  2014    4     24       23         5        0      0
6  2015    2     11       42         4        0      0
'data.frame':       453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : num  2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : int  1 0 0 0 0 0 0 0 0 0 ...
$ Snow       : num  0 0 0 0 0 0 0 0 0 0 ...
```

## <a name="prepare-the-data"></a>데이터 준비

이 샘플 데이터베이스에서는 대부분의 준비가 이미 수행되었지만 여기서 준비 작업을 하나 더 수행합니다.
다음 R 스크립트를 사용하고 데이터 형식을 *비율*로 변경하여 세 개의 열을 *범주*로 식별합니다.



```r
#Changing the three factor columns to factor types
rentaldata$Holiday <- factor(rentaldata$Holiday);
rentaldata$Snow    <- factor(rentaldata$Snow);
rentaldata$WeekDay <- factor(rentaldata$WeekDay);



#Visualize the dataset after the change
str(rentaldata);
```

다음과 비슷한 결과가 표시됩니다.

```results
data.frame':      453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : Factor w/ 7 levels "1","2","3","4",..: 2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : Factor w/ 2 levels "0","1": 2 1 1 1 1 1 1 1 1 1 ...
$ Snow       : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...
```

이제 해당 데이터를 학습에 사용할 준비가 되었습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행할 생각이 없으면 TutorialDB 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 2부에서는 다음 작업을 수행하는 방법을 알아보았습니다.

* R 데이터 프레임에 샘플 데이터 로드
* 일부 열을 범주로 식별하여 R에서 데이터 준비

TutorialDB 데이터베이스의 데이터를 사용하는 기계 학습 모델을 만들려면 다음 자습서 시리즈의 3부를 수행합니다.

> [!div class="nextstepaction"]
> [R에서 SQL 기계 학습을 사용하여 예측 모델 만들기](r-predictive-model-train.md)
