---
title: SQL을 사용한 데이터 관찰 및 탐색(연습) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b933337c1234f09f0a8963c1979a86a9ab61db53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201735"
---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>SQL을 사용한 데이터 관찰 및 탐색(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 탐색은 데이터 모델링의 중요한 한 부분이며 분석에 사용되는 데이터의 요약 정보를 검토하고 데이터를 시각화하는 작업을 포함합니다. 이 단원에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 과 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에 포함된 R 함수 모두를 사용해서 데이터 개체를 탐색하고 플롯을 생성합니다.

그런 다음 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 로 설치된 패키지에서 제공되는 새로운 함수를 사용하여 데이터를 시각화하는 플롯을 생성합니다.

> [!TIP]
> 이미 R을 잘 안다면?
>   
> 모든 데이터를 다운로드하고 필요한 환경이 준비되었으므로 RStudio나 다른 환경에서 전체 R 스크립트를 실행하고 직접 그 기능을 살펴볼 수 있습니다. RSQL_Walkthrough.R 파일을 열고 각 줄을 실행하거나 전체 스크립트를 데모로 실행합니다.
>   
> RevoScaleR 함수에 대한 추가 설명과 R에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 작업에 대한 팁을 얻으려면 자습서를 계속 진행합니다. 정확히 동일한 스크립트를 사용합니다.

## <a name="verify-downloaded-data-using-sql-server"></a>SQL Server를 사용하여 다운로드한 데이터 확인

먼저 데이터가 올바르게 로드되었는지 확인합니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Visual Studio의 서버 탐색기, Visual Studio Code 와 같이 선호하는 데이터베이스 관리 도구를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.


2. 새로 만든 데이터베이스를 선택하고 확장해서 새 데이터베이스, 테이블, 함수를 확인합니다.
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  데이터가 올바르게 로드되었는지 확인하기 위해 테이블을 마우스 오른쪽 클릭하고 **상위 1000 개 행 선택** 을 선택합니다. 아래 쿼리가 실행됩니다. 메뉴 옵션은이 쿼리를 실행합니다.

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    테이블의 데이터가 보이지 않는 경우 이전 항목의 [문제 해결](walkthrough-prepare-the-data.md) 절을 참조합니다.

4. 이 데이터 테이블은 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md) 를 추가해서 집합 기반 계산용으로 최적화되었습니다. 아래 문을 실행해서 테이블에 대한 빠른 요약을 생성합니다.

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    다음 단원에서는 R을 사용하여 좀 더 복잡한 요약을 생성합니다.

## <a name="next-lesson"></a>다음 단원

[R을 사용한 데이터 요약](walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>이전 단원

[PowerShell을 사용한 데이터 준비](walkthrough-prepare-the-data.md)
