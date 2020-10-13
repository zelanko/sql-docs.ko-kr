---
description: 프로젝트 설정 (변환) (AccessToSQL)
title: 프로젝트 설정 (변환) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 63952d4e46b1c25e49e7f29f8da1e23543232cb7
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988519"
---
# <a name="project-settings-conversion-accesstosql"></a>프로젝트 설정 (변환) (AccessToSQL)
변환 프로젝트 설정을 사용 하 여 개체를 Access 데이터베이스 개체에서 또는 Azure SQL Database 개체로 변환 하는 방법을 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
변환 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   **프로젝트 설정** 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 변환 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 선택 합니다.  
  
-   **기본 프로젝트 설정** 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 변환 설정에 액세스 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고, 설정을 확인 해야 하 **는 마이그레이션 프로젝트 형식 드롭다운을** 선택 하 고, 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 선택 합니다.  
  
## <a name="options"></a>옵션  
**기본 키 추가**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]액세스 테이블에 기본 키 또는 고유 인덱스가 없는 경우 또는 SQL Azure 테이블에 새 기본 키를 만듭니다.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
SQL Azure에 연결 된 경우 기본적으로 True입니다. **타임 스탬프 열 추가**  
필요한 경우 SSMA가 타임 스탬프 값을 만들어야 하는지 여부를 지정 합니다.  
  
-   **기본 모드**: ssma 결정 허용  
  
-   **낙관적 모드**: 없음  
  
-   **전체 모드**: ssma 결정 허용  
  
**변환 평가 보고서와 함께 데이터 평가 보고서 포함**  
평가 보고서에 데이터 평가를 포함 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**기본 키에 null 허용 열이 포함 된 경우의 메시지 유형**  
Null을 허용 하는 열이 포함 된 기본 키를 찾을 때 SSMA에서 출력 창에 표시 하는 메시지 유형 (경고, 오류 또는 없음)을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**외래 키 열의 크기가 다른 경우의 메시지 유형**  
잘못 된 텍스트 외래 키를 찾을 때 SSMA에서 출력 창에 표시 하는 메시지 유형 (경고, 오류 또는 없음)을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**메모 열이 인덱싱되는 경우의 메시지 유형**  
**메모** 열이 포함 된 인덱스를 찾을 때 Ssma에서 출력 창에 표시 하는 메시지 유형 (경고, 오류 또는 없음)을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**복잡 한 쿼리가 와일드 카드를 사용 하는 경우 경고 ( \& #42;)**  
SELECT 문의 열 이름이 와일드 카드 (*) 인 경우 출력 창에 경고를 표시 하 고 오류 목록 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자 이름이 변경 되 면 경고**  
SSMA에서 개체 식별자 이름을 변경할 때 평가 보고서와 출력 창에 메시지를 표시 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자를 따옴표로 묶을 때 경고**  
SSMA에서 개체 식별자 이름을 따옴표로 묶을 때 평가 보고서와 출력 창에 메시지를 표시 합니다. 이름이 키워드 이거나 특수 문자를 포함 하는 경우에는 식별자를 따옴표로 묶을 필요가 있습니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
## <a name="see-also"></a>참고 항목  
[사용자 인터페이스 참조 (액세스)](./user-interface-reference-accesstosql.md)  
