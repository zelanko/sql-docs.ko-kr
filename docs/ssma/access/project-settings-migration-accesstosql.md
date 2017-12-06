---
title: "프로젝트 설정 (마이그레이션) (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7fcf9092c57fd07601171003381812de2ed6b12
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-migration-accesstosql"></a>프로젝트 설정 (마이그레이션) (AccessToSQL)
마이그레이션 프로젝트 설정으로 데이터가 마이그레이션되는 방식을 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
마이그레이션 창도에서 사용할 수는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자.  
  
-   사용 하 여는 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 마이그레이션 설정에 액세스 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **마이그레이션**합니다.  
  
-   사용 하 여 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 마이그레이션 설정에 액세스 하려면는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 라는 프로젝트 형식을 선택 **마이그레이션 대상 버전** 콤보 상자 설정에 액세스를 클릭 합니다. 원하는는 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **마이그레이션**합니다.  
  
## <a name="options"></a>옵션  
**CHECK 제약 조건**  
테이블에 데이터를 추가할 때 SSMA 제약 조건을 확인 해야 하는지 여부를 지정 합니다.  
  
-   **기본 모드**: False  
  
-   **최적 모드**: True  
  
-   **전체 모드**: False  
  
**트리거 실행**  
데이터를 추가 하면 SSMA 삽입 트리거를 발생 시켜야 하는지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 테이블입니다.  
  
-   **기본 모드**: False  
  
-   **최적 모드**: True  
  
-   **전체 모드**: False  
  
**ID 유지**  
데이터를 추가 하면 SSMA 액세스 id 값을 유지할지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이 값이 False [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] id 값을 할당 합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: True  
  
-   **전체 모드**: False  
  
**Null 유지**  
데이터를 추가 하면 SSMA 원본 데이터에 null 값을 유지할지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에 지정 된 기본값에 관계 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
**테이블 잠금**  
SSMA 데이터 마이그레이션 중에 테이블에 데이터를 추가할 때 테이블 잠금 여부를 지정 합니다. 값이 False 이면 SSMA 행 잠금을 사용 합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: True  
  
-   **전체 모드**: True  
  
**지원 되지 않는 날짜를 대체 합니다.**  
SSMA 이전 가장 빠른 버전의 액세스 날짜를 수정 해야 하는지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] datetime 날짜 (1753 01 년 1 월).  
  
-   현재 날짜 값을 유지 하기 위해 선택 **아무 작업도 수행 하지**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]datetime 열에는 1753 년 1 월 1 일 이전의 날짜를 수락 하지 않습니다. 오래 된 날짜를 사용 하 여 문자 값을 날짜/시간 값을 변환 해야 합니다.  
  
-   1753 년 1 월 1 일 이전의 날짜를 NULL로 변환 하려면 선택 **NULL로 대체**합니다.  
  
-   1753 년 1 월 1 일 이전 날짜는 지원 되는 날짜를 바꾸려면 선택 **지원 되는 날짜에 가장 가까운 바꿉니다**합니다. 가장 가까운 기본적으로이 값을 선택 하는 경우 지원 되는 날짜는 1753 년 1 월 1 일으로 선택 됩니다.  
  
**일괄 처리 크기**  
데이터 마이그레이션 중에 사용 되는 일괄 처리 크기입니다. 각 일괄 처리 후 트랜잭션이 기록 됩니다. 기본적으로 모든 스키마에 대 한 일괄 처리 크기는 10000입니다.  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
