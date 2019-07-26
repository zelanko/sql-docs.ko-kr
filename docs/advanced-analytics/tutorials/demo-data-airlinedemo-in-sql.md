---
title: Python 및 R 자습서 SQL Server에 대 한 항공 비행 데모 데이터 집합
Description: R 및 Python에서 항공편 데이터 집합을 포함 하는 데이터베이스를 만듭니다. 이 데이터 집합은 SQL Server 저장 프로시저에서 R 언어 또는 Python 코드를 래핑하는 방법을 보여 주는 연습에 사용 됩니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 38e61bcbf3a5ff5ed44f85d5ad28406550e5a726
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469681"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Python 및 R 자습서 SQL Server에 대 한 항공 비행 도착 데모 데이터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 연습에서는 R 또는 Python 기본 제공 항공 데모 데이터 집합에서 가져온 데이터를 저장 하는 SQL Server 데이터베이스를 만듭니다. R 및 Python 배포는 Management Studio를 사용 하 여 SQL Server 데이터베이스로 가져올 수 있는 동일한 데이터를 제공 합니다.

이 연습을 완료 하려면 T-sql 쿼리를 실행할 수 있는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 다른 도구가 있어야 합니다.

이 데이터 집합을 사용 하는 자습서 및 빠른 시작에는 다음이 포함 됩니다.

+  [Revoscalepy를 사용 하 여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작 하 고 R 또는 Python 통합을 포함 하는 데이터베이스 엔진 인스턴스에 연결 합니다.  

2. 개체 탐색기에서 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **flightdata**라는 새 데이터베이스를 만듭니다.

3. **Flightdata**를 마우스 오른쪽 단추로 클릭 하 고 **작업**, **플랫 파일 가져오기**를 차례로 클릭 합니다.

4. 설치 된 언어에 따라 R 또는 Python 배포에 제공 된 어 락 Linedemodata .csv 파일을 엽니다.

   R의 경우 C:\Program Files\Microsoft SQL Server\MSSQL14.에서 **락 Linedemosmall .csv** 를 찾습니다. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Python의 경우 C:\Program **Linedemosmall .csv** 에서 C:\PROGRAM Files\Microsoft SQL Server\MSSQL14.를 찾습니다. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
파일을 선택 하면 테이블 이름 및 스키마에 대 한 기본값이 채워집니다.

  ![비행기 데모 기본값을 표시 하는 플랫 파일 가져오기 마법사](media/import-airlinedemosmall.png)

나머지 페이지를 클릭 하 고 기본값을 적용 하 여 데이터를 가져옵니다.


## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행 하 여 데이터가 업로드 되었는지 확인 합니다.

1. 개체 탐색기의 데이터베이스에서 **flightdata** 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>다음 단계

다음 단원에서는이 데이터를 기반으로 선형 회귀 모델을 만듭니다.

+ [Revoscalepy를 사용 하 여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)
