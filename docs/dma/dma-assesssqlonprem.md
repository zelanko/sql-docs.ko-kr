---
title: "(데이터 Migration Assistant)는 SQL Server 마이그레이션 평가 수행 | Microsoft Docs"
ms.custom: 
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c23f8d37e7af9daad2af78164a21adbe8c613a3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="perform-a-sql-server-migration-assessment"></a>SQL Server 마이그레이션 평가 수행
단계별 지침을 통해 온-프레미스 SQL Server, 데이터 마이그레이션 길잡이 사용 하 여 Azure SQL 데이터베이스 또는 Azure VM에서 실행 중인 SQL Server로 마이그레이션하기 위한 첫 번째 평가 수행할 수 수 있습니다.

## <a name="create-an-assessment"></a>평가 만들기

1.  선택 된 **새로** (+) 아이콘을 선택 합니다는 **평가** 프로젝트 형식을 합니다.

2.  원본 및 대상 서버 유형을 설정 합니다.

    온-프레미스 SQL Server 인스턴스를 최신 온-프레미스 SQL Server 인스턴스 또는 Azure VM에서 호스팅되는 SQL Server 업그레이드 하는 경우 원본 및 대상 서버 유형으로 설정 **SQL Server**합니다. Azure SQL 데이터베이스를 마이그레이션하는 경우 대신 대상 서버 유형으로 설정 **Azure SQL 데이터베이스**합니다.

3.  **만들기**를 클릭합니다.

    ![평가 만들기](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>평가 옵션 선택

1. 대상 SQL Server 버전으로 마이그레이션하도록 계획을 선택 합니다.

2. 보고서 유형을 선택 합니다.

   대상 Azure VM에서 호스팅되는 SQL Server 또는 온-프레미스 SQL Server로 마이그레이션하는 중에 대 한 원본 SQL Server 인스턴스를 평가 하는 경우에 다음 평가 보고서 유형 중 하나 또는 모두를 선택할 수 있습니다.

    -   **호환성 문제**

    -   **새로운 기능 권장 사항**

    ![SQL Server 대상에 대 한 평가 보고서 형식을 선택 합니다.](../dma/media/AssessmentTypes.png)

   Azure SQL 데이터베이스로 마이그레이션에 대 한 원본 SQL Server 인스턴스를 평가 하는 경우에 다음 평가 보고서 유형 중 하나 또는 모두를 선택할 수 있습니다.

    -   **데이터베이스 호환성 확인**

    -   **기능 패리티를 확인 합니다.**

    ![대상 SQL 데이터베이스에 대 한 평가 보고서 유형 선택](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>평가 하기 위해 데이터베이스를 추가 합니다.

1.  선택 **추가 소스** 연결 플라이 아웃 메뉴를 엽니다.

2.  SQL server 인스턴스 이름을 입력, 인증 형식을 선택 하 고, 올바른 연결 속성을 설정 하 고 다음 선택 **연결**합니다.

3.  데이터베이스를 평가, 선택한 후 선택 **추가**합니다.

    > [!NOTE] 
    > Shift 또는 Ctrl 키를 누른 채로 한 다음 클릭 하는 동안 선택 하 여 여러 데이터베이스를 제거할 수 **제거 소스**합니다. 사용 하 여 여러 SQL Server 인스턴스 간에 데이터베이스를 추가할 수도 있습니다는 **추가 소스** 단추입니다.

4.  클릭 **다음** 평가 시작 합니다.

    ![소스를 추가 하 고 평가 시작 합니다.](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>결과 보기

평가 기간 동안 추가 된 데이터베이스 수와 각 데이터베이스의 스키마 크기에 따라 달라 집니다. 으로 사용할 수 있는 각 데이터베이스에 대 한 결과가 표시 됩니다.

1.  평가, 완료 된 데이터베이스를 선택한 다음 사이 전환 **호환성 문제** 및 **권장 기능** 전환기를 사용 하 여 합니다.

2.  모든 호환성 수준에서 대상 SQL Server 버전에서 지 원하는에서 선택한 호환성 문제를 검토는 **옵션** 페이지.

영향을 받는 개체에서 식별 된 모든 문제에 대 한 세부 정보를 분석 하 여 호환성 문제를 검토할 수 있습니다 **주요 변경 내용**, **동작 변경 내용**, 및 **사용 되지 않는 기능** .

![평가 결과 보기](../dma/media/ReviewResults.png)

마찬가지로, 간에 기능 권장 사항을 검토할 수 있습니다 **성능**, **저장소**, 및 **보안** 영역입니다.

기능 권장 사항을 다양 한 메모리 내 OLTP와 Columnstore, 스트레치 데이터베이스, 상시 암호화, 동적 데이터 마스킹 및 투명 한 데이터 암호화와 같은 기능을 다룹니다.

![보기 기능 권장 사항](../dma/media/FeatureRecommendations.png)

Azure SQL 데이터베이스에 대 한 평가 마이그레이션 차단 문제 및 기능 패리티 문제를 제공합니다. 태그별 옵션을 선택 하 여 두 범주에 대 한 결과 검토 합니다.

- **대응 되는 SQL Server 기능** 범주 다양 한 권장 사항, Azure 및 완화 단계에서 사용할 수 있는 대안을 제공 합니다. 마이그레이션 프로젝트에서 이러한 노력을 계획할 수 있습니다.

  ![대응 되는 SQL Server 기능에 대 한 정보 보기](../dma/media/SQLFeatureParity.png)

- **호환성 문제** 범주 Azure SQL 데이터베이스에 온-프레미스 SQL Server 데이터베이스 마이그레이션를 차단 하는 부분적으로 지원 되거나 지원 되지 않는 기능을 제공 합니다. 그러한 문제를 해결 하기 위한 권장 사항을 제공 합니다.

  ![보기 호환성 문제](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>결과 내보내기

모든 데이터베이스 평가에서는 완료 된 후 선택 **보고서 내보내기** JSON 파일이 나 CSV 파일에 결과 내보내려면 합니다. 사용자 고유의 편의 위해 데이터를 분석할 수 있습니다.

동시에 여러 평가 실행 하 고 열어 평가 상태를 볼 수는 **모든 평가** 페이지.
