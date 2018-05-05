---
title: 프로젝트 설정 (변환) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f5e2bb08277adfcb2a4d609a92a726db6220552d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-conversion-accesstosql"></a>프로젝트 설정 (변환) (AccessToSQL)
변환 프로젝트 설정 개체에서 Access 데이터베이스 개체를 변환 하는 방법을 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 개체입니다.  
  
변환에서 제공 되는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자.  
  
-   사용 하 여는 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 변환 설정에 액세스 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
-   사용 하 여 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 변환 설정에 액세스 하려면는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 설정 된 볼 /에서 변경 하는 데 필요한 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운을 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
## <a name="options"></a>옵션  
**기본 키를 추가 합니다.**  
새 기본 키를 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Access 테이블에 기본 키 또는 고유 인덱스 일 경우 SQL Azure 테이블입니다.  
  
-   **기본 모드**: False  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
SQL Azure에 연결 되어 있을 때 True 기본적입니다. **타임 스탬프 열 추가**  
필요한 경우 SSMA 타임 스탬프 값을 만들 해야 하는지 여부를 지정 합니다.  
  
-   **기본 모드**: SSMA 수 결정  
  
-   **최적 모드**: 하지  
  
-   **전체 모드**: SSMA 수 결정  
  
**변환 평가 보고서와 함께 데이터 평가 보고서를 포함 합니다.**  
평가 보고서에 데이터 평가 포함합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
**기본 키에 null 허용 열이 포함 된 경우 메시지 유형**  
SSMA는 null 허용 열에 기본 키를 발견 하면 출력 창에 표시 된 메시지 (경고, 오류 또는 Nothing)의 유형을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **최적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**외래 키 열은 다양 한 크기의 경우 메시지 유형**  
잘못 된 텍스트 외래 키를 발견 하면 SSMA 출력 창에 표시 된 메시지 (경고, 오류 또는 Nothing)의 유형을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **최적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**메모 열이 인덱싱된 경우 메시지 유형**  
메시지 (경고, 오류 또는 Nothing)를 포함 하는 인덱스를 발견 하면 출력 창에 표시 되는 SSMA의 유형을 지정는 **메모** 열입니다.  
  
-   **기본 모드**: 경고  
  
-   **최적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**복잡 한 쿼리는 와일드 카드를 사용 하는 경우 경고 (\&#42;)**  
SELECT 문에서 열 이름이 와일드 카드 (*) 일 때 출력 창 및 오류 목록에 경고를 표시 합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자 이름이 변경 되 면 경으십시오**  
SSMA가 개체 식별자 이름을 변경할 때 메시지를 출력 창 및 평가 보고서에 표시 합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자 인용 됩니다 때 경으십시오**  
개체 식별자 이름이 SSMA 여 인용 됩니다 때 메시지를 출력 창 및 평가 보고서에 표시 합니다. 따옴표 식별자 이름에는 키워드 또는 특수 문자를 포함 하는 경우 반드시 합니다.  
  
-   **기본 모드**: True  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
