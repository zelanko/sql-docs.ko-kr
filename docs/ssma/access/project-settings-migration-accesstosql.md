---
title: 프로젝트 설정 (마이그레이션) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c8cec81d0e6281ce9f57d9d689bd5dfdc2d6feb1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738211"
---
# <a name="project-settings-migration-accesstosql"></a>프로젝트 설정 (마이그레이션) (AccessToSQL)
마이그레이션 프로젝트 설정을 통해로 데이터가 마이그레이션되는 방식을 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
마이그레이션 창에서 사용할 수는 **프로젝트 설정** 하 고 **기본 프로젝트 설정** 대화 상자.  
  
-   사용 된 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 마이그레이션 설정에 액세스 하려면 합니다 **도구** 메뉴에서 **프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에  **마이그레이션**합니다.  
  
-   사용 된 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 마이그레이션 설정에 액세스 하려면 합니다 **도구** 메뉴에서 **기본 프로젝트 설정**, 프로젝트 형식을 선택 **마이그레이션 대상 버전** 는 콤보 상자 있습니다 설정에 액세스 하려면 클릭 **일반적인** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **마이그레이션**합니다.  
  
## <a name="options"></a>변수  
**CHECK 제약 조건**  
SSMA 데이터 테이블에 추가할 때 제약 조건을 확인 해야 하는지 지정 합니다.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**트리거 실행**  
데이터를 추가할 때 SSMA 삽입 트리거를 실행 해야 하는지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**ID 유지**  
데이터를 추가할 때 SSMA 액세스 id 값을 유지할지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 값이 False 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] id 값을 할당 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**Null 유지**  
데이터를 추가할 때 SSMA 원본 데이터의 null 값을 유지할지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지정 된 기본값에 관계 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**테이블 잠금**  
데이터 마이그레이션 중 데이터 테이블에 추가할 때 SSMA 테이블 잠금 여부를 지정 합니다. 값이 False 이면 SSMA는 행 잠금을 사용 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: True  
  
**지원 되지 않는 날짜를 대체 합니다.**  
SSMA 이전 가장 이전 버전의 액세스 날짜를 수정 해야 하는지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 날짜 (1753 01 년 1 월).  
  
-   현재 날짜 값을 유지 하려면 선택 **아무 작업도 수행**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 1753 년 1 월 1 일 이전의 날짜를 datetime 열에서 허용 하지 않습니다. 이전 날짜를 사용 하 여 문자 값을 datetime 값 변환 해야 합니다.  
  
-   1753 년 1 월 1 일 이전의 날짜를 NULL로 변환 하려면 **NULL 바꿉니다**합니다.  
  
-   지원 되는 날짜가 1753 년 1 월 1 일 이전의 날짜를 바꾸려면 선택 **지원 되는 날짜에 가까운 바꿉니다**합니다. 가장 가까운 기본적으로이 값을 선택 하는 경우 지원 되는 날짜는 1753 년 1 월 01로 선택 됩니다.  
  
**일괄 처리 크기**  
데이터 마이그레이션 중에 사용 되는 일괄 처리 크기입니다. 각 일괄 처리 후 트랜잭션이 기록 됩니다. 기본적으로 모든 스키마에 대 한 일괄 처리 크기는 10000입니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
