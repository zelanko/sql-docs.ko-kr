---
title: "보기 및 SQL (연습)를 사용 하 여 데이터를 탐색 | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 33
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f531d6b3bd3732c6c4d8c257561a3b3c5c865f2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>보기 및 SQL (연습)를 사용 하 여 데이터를 탐색 합니다.

데이터 탐색은 데이터 모델링의 중요한 부분이며 분석에 사용할 데이터 개체의 요약 및 데이터 시각화 검토를 포함합니다. 이 단원에서는 데이터 개체를 탐색 하 고이 모두 사용 하 여 플롯을 생성할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 R 함수에 포함 된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다.

다음으로 설치 된 패키지에서 제공 하는 새 함수를 사용 하 여 데이터를 시각화 하는 점도 생성 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다.

> [!TIP]
> 이미 R을 잘 알고 있는 경우
>   
> 모든 데이터를 다운로드하고 환경을 준비했으므로 RStudio 또는 다른 환경에서 전체 R 스크립트를 실행하고 직접 기능을 살펴볼 수 있습니다. RSQL_Walkthrough.R 파일을 열고 개별 줄을 강조 표시하여 실행하거나 전체 스크립트를 데모로 실행합니다.
>   
> RevoScaleR 함수에 대한 추가 설명과 R에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하기 위한 팁을 얻으려면 자습서를 계속 진행합니다. 정확히 동일한 스크립트를 사용합니다.

## <a name="verify-downloaded-data-using-sql-server"></a>SQL Server를 사용 하 여 다운로드 한 데이터를 확인 합니다.

먼저 데이터가 올바르게 로드되었는지 확인합니다.

1. 에 연결 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같은 즐겨 찾는 데이터베이스 관리 도구를 사용 하 여 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Visual Studio 또는 Visual Studio Code에서 서버 탐색기.

2. 새 데이터베이스, 테이블 및 함수를 표시 하려면 확장을 만든 데이터베이스를 선택 합니다.
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  데이터 올바르게 로드 되었는지 확인 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 하려면 **상위 1000 개 행 선택**합니다. 메뉴 옵션은이 쿼리를 실행합니다.

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    테이블의 데이터가 보이지 않는 경우 이전 항목의 [문제 해결](/walkthrough-prepare-the-data.md) 섹션을 참조하세요.

4. 이 데이터 테이블은 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md)를 추가하는 방식으로 집합 기반 계산에 최적화되었습니다. 테이블에 대 한 정보를 빠르게 생성 하는이 문을 실행 합니다.

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    다음 단원에서는 R을 사용하여 더 복잡한 요약을 생성합니다.

## <a name="next-lesson"></a>다음 단원

[R을 사용 하 여 데이터를 요약 합니다.](/walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>이전 단원

[PowerShell을 사용 하 여 데이터 준비](/walkthrough-prepare-the-data.md)

