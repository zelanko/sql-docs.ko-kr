---
title: (Data Migration Assistant)는 SQL Server 마이그레이션 평가 수행 합니다. | Microsoft Docs
description: 다른 SQL Server로 또는 Azure SQL Database로 마이그레이션하기 전에 온-프레미스 SQL Server를 평가 하기 위해 Data Migration Assistant 사용 방법 알아보기
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: 463ada293202007eb92b6d3dfedc3c96c7d2f9f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060955"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 SQL Server 마이그레이션 평가 수행 합니다.

다음 단계별 지침을 온-프레미스 SQL Server Data Migration Assistant를 사용 하 여 Azure VM 또는 Azure SQL Database에서 실행 중인 SQL Server로 마이그레이션에 대 한 첫 번째 평가 수행 하는 데 도움이 됩니다.

## <a name="create-an-assessment"></a>평가 만들기

1.  선택 된 **새로 만들기** (+) 아이콘을 선택한 후는 **평가** 프로젝트 형식.

2.  원본 및 대상 서버 유형을 설정 합니다.

    최신 온-프레미스 SQL Server 인스턴스 또는 Azure VM에서 호스팅되는 SQL Server 온-프레미스 SQL Server 인스턴스를 업그레이드 하는 경우 원본 및 대상 서버 유형으로 설정 **SQL Server**합니다. Azure SQL Database로 마이그레이션하는 경우 대신로 대상 서버 유형 **Azure SQL Database**합니다.

3.  **만들기**를 클릭합니다.

    ![평가 만들기](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>평가 옵션 선택

1. 마이그레이션하려는 대상 SQL Server 버전을 선택 합니다.

2. 보고서 유형을 선택 합니다.

   대상 Azure VM에서 호스팅되는 SQL Server 또는 온-프레미스 SQL Server로 마이그레이션에 대 한 원본 SQL Server 인스턴스를 평가 하려는 경우 다음 평가 보고서 유형 중 하나 또는 모두를 선택할 수 있습니다.

    -   **호환성 문제**
    -   **새로운 기능의 권장 사항**

    ![SQL Server 대상에 대 한 평가 보고서 유형을 선택합니다](../dma/media/AssessmentTypes.png)

   Azure SQL Database로 마이그레이션에 대 한 원본 SQL Server 인스턴스를 평가할 때 다음 평가 보고서 유형 중 하나 또는 모두를 선택할 수 있습니다.

    -   **데이터베이스 호환성 확인**
    -   **기능 패리티 확인**

    ![SQL Database 대상에 대 한 평가 보고서 유형 선택](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>평가 하는 데이터베이스 추가

1.  선택 **소스 추가** 연결 플라이 아웃 메뉴를 엽니다.

2.  SQL server 인스턴스 이름을 입력, 인증 유형을 선택, 올바른 연결 속성을 설정 및 선택한 **Connect**합니다.

3.  데이터베이스를 평가 하 고 선택한 선택 **추가**합니다.

    > [!NOTE] 
    > Shift 또는 Ctrl 키를 누른 채로 클릭 하는 동안 선택 하 여 여러 데이터베이스를 제거할 수 있습니다 **제거 원본**합니다. 사용 하 여 여러 SQL Server 인스턴스에서 데이터베이스를 추가할 수도 있습니다는 **소스 추가** 단추입니다.

4.  클릭 **다음** 평가를 시작 합니다.

    ![소스를 추가 하 고 평가 시작 합니다.](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>결과 보기

평가 기간 추가 데이터베이스 수와 각 데이터베이스의 스키마 크기에 따라 달라 집니다. 사용할 수는 즉시 각 데이터베이스에 대 한 결과가 표시 됩니다.

1.  평가 완료 하는 데이터베이스를 선택한 다음 전환할 **호환성 문제** 하 고 **기능 권장 사항** 전환기를 사용 하 여 합니다.

2.  모든 호환성 수준에서 대상 SQL Server 버전에서 지 원하는에서 선택한 호환성 문제를 검토 합니다 **옵션** 페이지입니다.

영향을 받는 개체에서 해당 세부 정보 및 잠재적으로에서 식별 한 모든 문제에 대 한 수정 분석 하 여 호환성 문제를 검토할 수 있습니다 **주요 변경 내용**하십시오 **동작 변경 내용**, 및  **사용 되지 않는 기능**합니다.

![평가 결과 보기](../dma/media/ReviewResults.png)

마찬가지로, 기능 권장 사항에서 검토할 수 있습니다 **성능**를 **저장소**, 및 **보안** 영역입니다.

기능 권장 사항 다양 한 메모리 내 OLTP, Columnstore, Stretch Database, Always Encrypted, 동적 데이터 마스킹 및 투명 한 데이터 암호화와 같은 기능을 설명합니다.

![기능 권장 사항 보기](../dma/media/FeatureRecommendations.png)

Azure SQL Database에 대 한 평가가 마이그레이션 차단 문제와 기능 패리티 문제를 제공합니다. 특정 옵션을 선택 하 여 두 범주에 대 한 결과 검토 합니다.

- 합니다 **SQL Server 기능 패리티** 범주는 다양 한 권장 사항, Azure 및 완화 단계에서 사용할 수 있는 대안을 제공 합니다. 마이그레이션 프로젝트에서이 노력을 계획할 수 있습니다.

  ![SQL Server 기능 패리티에 대 한 정보 보기](../dma/media/SQLFeatureParity.png)

- 합니다 **호환성 문제** 범주는 Azure SQL database로 온-프레미스 SQL Server 데이터베이스 마이그레이션 차단 하는 부분적으로 지원 되거나 지원 되지 않는 기능을 제공 합니다. 그런 다음 해당 문제를 해결 하기 위한 권장 사항을 제공 합니다.

  ![보기 호환성 문제](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>결과 내보내기

모든 데이터베이스 평가 완료 한 후 선택 **보고서 내보내기** 에 JSON 파일 또는 CSV 파일에 결과 내보냅니다. 그런 다음 고유한 편의 위해 데이터를 분석할 수 있습니다.

동시에 여러 평가 실행 하 고 열어서 평가 상태를 볼 수는 **모든 평가** 페이지입니다.
