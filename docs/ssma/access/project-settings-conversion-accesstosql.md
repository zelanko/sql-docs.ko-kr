---
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: df03cfe48fe66b359cb9ec054a82b24b4a8ce3dc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783782"
---
# <a name="project-settings-conversion-accesstosql"></a>프로젝트 설정 (변환) (AccessToSQL)
변환 프로젝트 설정을 통해 개체에서 Access 데이터베이스 개체를 변환 하는 방법을 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 개체입니다.  
  
변환 창에서 사용할 수는 **프로젝트 설정** 하 고 **기본 프로젝트 설정** 대화 상자.  
  
-   사용 된 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 변환 설정에 액세스 하려면 합니다 **도구** 메뉴에서 **프로젝트 설정**, 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에  **변환**합니다.  
  
-   사용 된 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 변환 설정에 액세스 하는 **도구** 메뉴에서 **기본 프로젝트 설정**, 설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택  **마이그레이션 대상 버전** 드롭다운을 클릭 **일반** 한 다음 선택한 왼쪽된 창의 맨 아래에 **변환**합니다.  
  
## <a name="options"></a>변수  
**기본 키를 추가 합니다.**  
새 기본 키를 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블 액세스 테이블을 기본 키 또는 고유 인덱스에 있는 경우.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
SQL Azure 연결할 때 기본적으로 True입니다. **타임 스탬프 열 추가**  
필요한 경우 SSMA 타임 스탬프 값을 만들 해야 하는지 여부를 지정 합니다.  
  
-   **기본 모드**: SSMA 수 결정  
  
-   **낙관적 모드**: 없습니다  
  
-   **전체 모드**: SSMA 수 결정  
  
**변환 평가 보고서를 사용 하 여 데이터 평가 보고서를 포함 합니다.**  
평가 보고서에 데이터 평가 포함합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**기본 키에 null 허용 열에 포함 된 경우 메시지 유형**  
SSMA null 허용 열을 사용 하 여 기본 키를 발견 하면 출력 창에 표시 하는 메시지 (경고, 오류 또는 아무 것도)의 형식을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**외래 키 열 다양 한 크기의 경우 메시지 유형**  
SSMA는 잘못 된 텍스트 외래 키를 발견 하면 출력 창에 표시 하는 메시지 (경고, 오류 또는 아무 것도)의 형식을 지정 합니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**메모 열이 인덱싱 될 때 메시지 형식**  
SSMA를 포함 하는 인덱스를 발견 하면 출력 창에서 보여 주는 메시지 (경고, 오류 또는 아무 것도)의 형식을 지정 된 **메모** 열입니다.  
  
-   **기본 모드**: 경고  
  
-   **낙관적 모드**: 메시지 없음  
  
-   **전체 모드**: 오류  
  
**복잡 한 쿼리를 와일드 카드를 사용 하는 경우 경고 (\&#42;)**  
SELECT 문에서 열 이름을 와일드 카드 (*) 하는 경우 출력 창과 오류 목록에서 경고를 표시 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자 이름 변경 될 때 경고 합니다.**  
SSMA에서 개체 식별자 이름이 변경 될 때 출력 창에서 평가 보고서에 메시지를 표시 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**식별자는 따옴표로 묶어야 하는 경우 경으십시오**  
SSMA에서 개체 식별자 이름을 따옴표로 묶을 수는 경우 메시지를 출력 창에서 평가 보고서에 표시 합니다. 따옴표 식별자 이름을 키워드 또는 특수 문자를 포함 하는 경우 반드시 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
