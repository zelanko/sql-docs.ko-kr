---
title: 자습서에 대한 항공 비행 데모 데이터
Description: R 및 Python에서 Airline 데이터 세트를 포함하는 데이터베이스를 만듭니다. 이 데이터 세트는 SQL Server Machine Learning Services용 R 및 Python 자습서에서 사용됩니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4f697287bff5ad4734d11c3d6391154a3a970470
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728004"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 및 R 자습서에 대한 항공 비행 도착 데모 데이터
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 연습에서는 R 또는 Python 기본 제공 Airline 데모 데이터 세트에서 가져온 데이터를 저장할 SQL Server 데이터베이스를 만듭니다. R 및 Python 배포는 Management Studio를 사용하여 SQL Server 데이터베이스로 가져올 수 있는 동일한 데이터를 제공합니다.

이 연습을 완료하려면 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 T-SQL 쿼리를 실행할 수 있는 다른 도구가 있어야 합니다.

이 데이터 세트를 사용하는 자습서 및 빠른 시작에는 다음이 포함됩니다.

+  [revoscalepy를 사용하여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작하고 R 또는 Python 통합을 포함하는 데이터베이스 엔진 인스턴스에 연결합니다.  

2. 개체 탐색기에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **flightdata**라는 새 데이터베이스를 만듭니다.

3. **flightdata**를 마우스 오른쪽 단추로 클릭하고, **작업** 및 **플랫 파일 가져오기**를 차례로 클릭합니다.

4. 설치한 언어에 따라 R 또는 Python 배포에 제공된 AirlineDemoData.csv 파일을 엽니다.

   R의 경우 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData에서 **AirlineDemoSmall.csv**를 찾습니다.
   
   Python의 경우 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data에서 **AirlineDemoSmall.csv**를 찾습니다.
  
파일을 선택하면 테이블 이름 및 스키마에 대한 기본값이 채워집니다.

  ![airline 데모 기본값을 표시하는 플랫 파일 가져오기 마법사](media/import-airlinedemosmall.png)

나머지 페이지를 클릭하고 기본값을 적용하여 데이터를 가져옵니다.


## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행하여 데이터가 업로드되었는지 확인합니다.

1. 개체 탐색기의 데이터베이스에서 **flightdata** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 새 쿼리를 시작합니다.

2. 몇 가지 간단한 쿼리를 실행합니다.

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>다음 단계

다음 단원에서는 이 데이터를 기반으로 선형 회귀 모델을 만듭니다.

+ [revoscalepy를 사용하여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)
