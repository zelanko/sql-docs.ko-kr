---
title: 항공사 항공편 도착 및 지연 SQL Server Python 및 R 자습서에 대 한 데이터 집합을 데모 | Microsoft Docs
Description: Create a database containing the Airline dataset from R and Python. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2ba431ecbc4f7d63415fdf6b351c5135ed0cdd8d
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49947449"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 및 R 자습서 항공사 비행 도착 데모 데이터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습에서는 R 또는 Python 기본 제공 Airline demo 데이터 집합에서 가져온된 데이터를 저장 하기 위한 SQL Server 데이터베이스를 만듭니다. R 및 Python 배포판 Management Studio를 사용 하 여 SQL Server 데이터베이스로 가져올 수 있는 동일한 데이터를 제공 합니다.

이 연습을 완료 하려면 있어야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 T-SQL 쿼리를 실행할 수 있는 다른 도구입니다.

이 데이터 집합을 사용 하 여 퀵 스타트 및 자습서에는 다음과 같습니다.

+  [Revoscalepy를 사용 하 여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작, R 또는 Python 통합이 있는 데이터베이스 엔진 인스턴스에 연결 합니다.  

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 **데이터베이스** 라는 새 데이터베이스를 만들고 **flightdata**합니다.

3. 마우스 오른쪽 단추로 클릭 **flightdata**, 클릭 **태스크**, 클릭 **플랫 파일 가져오기**합니다.

4. 설치 언어에 따라 R 또는 Python 배포에 제공 된 AirlineDemoData.csv 파일을 엽니다.

   R에 대 한 찾습니다 **AirlineDemoSmall.csv** C:\Program Files\Microsoft SQL Server\MSSQL14에서. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Python의 경우 찾습니다 **AirlineDemoSmall.csv** C:\Program Files\Microsoft SQL Server\MSSQL14에서. MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
파일을 선택 하면 테이블 이름 및 스키마에 대 한 기본 값으로 채워집니다.

  ![플랫 파일 가져오기 마법사 airline demo 기본값 표시](media/import-airlinedemosmall.png)

데이터를 가져오는 기본값을 적용 하 고 나머지 페이지를 클릭 합니다.


## <a name="query-the-data"></a>데이터를 쿼리 합니다.

유효성 검사 단계로, 데이터가 업로드 되었는지 확인 하는 쿼리를 실행 합니다.

1. 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 합니다 **flightdata** 데이터베이스 및 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>다음 단계

다음 단원에서는이 데이터를 기반으로 선형 회귀 모델을 만들게 됩니다.

+ [Revoscalepy를 사용 하 여 Python 모델 만들기](use-python-revoscalepy-to-create-model.md)
