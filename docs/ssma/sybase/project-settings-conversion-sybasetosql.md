---
title: 프로젝트 설정 (변환) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1d2f1c02b9a9400236381cdd30fb3deb570500c1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934659"
---
# <a name="project-settings-conversion-sybasetosql"></a>프로젝트 설정(변환)(SybaseToSQL)
**프로젝트 설정** 대화 상자의 변환 페이지에는 Ssma에서 Sybase (Sybase Server Enterprise) 구문을 또는 SQL Azure 구문으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
변환 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   모든 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 클릭 합니다.  
  
## <a name="miscellaneous-options"></a>기타 옵션  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 및 ASE는 서로 다른 오류 코드를 사용 합니다.  
  
이 설정을 사용 하 여 ASE 코드의 **@ @ERROR ** 에 대 한 참조가 발견 될 때 ssma에서 출력 또는 오류 목록 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.  
  
-   변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 문을 변환 하 고 경고 주석으로 표시 합니다.  
  
-   **표시를 오류로 표시**를 선택 하면 ssma는 변환을 건너뛰고 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 경고를 사용 하 여 변환 및 표시  
  
**전체 모드:** 오류로 표시  
  
**LIKE 연산자의 변환**  
Sybase ASE 동작과 일치 하도록 LIKE 피연산자를 변환할지 여부를 지정 합니다. Point는 Sybase가 like 패턴의 후행 공백을 잘라내는 것입니다. 해결 방법은 최대 전체 자릿수를 사용 하 여 고정 길이 데이터 형식으로 오른쪽 식을 캐스트 하는 것입니다.  
  
-   수정 하지 않고 식을 변환 하려면 **단순 변환** 을 선택 합니다.  
  
-   ASE 동작을 사용 하려면 **고정 길이로 캐스트를 선택 합니다.**  
  
모드 상자에서 변환 모드를 선택 하면 SSMA가 다음 설정을 적용 합니다.  
  
**기본/낙관적 모드**: 간단한 변환  
  
**전체 모드**: 고정 길이로 캐스트  
  
**빈 문자열을 숫자 형식으로 변환 또는 캐스팅**  
숫자 형식이 datatype 인수인 CONVERT 또는 CAST 식 내에서 빈 문자열 또는 빈 문자열을 처리 하는 방법을 지정 합니다. 이 설정에 사용할 수 있는 옵션은 다음과 같습니다.  
  
-   수정 하지 않고 식을 변환 하려면 **단순 변환** 을 선택 합니다.  
  
-   **빈 문자열을 0으로** 선택한 경우 문자열 매개 변수 {s}가 "" then 0 else {s} 끝 식 인 case ltrim (rtrim ({s}))으로 바뀝니다.  
  
모드 상자에서 변환 모드를 선택 하면 SSMA가 다음 설정을 적용 합니다.  
  
**기본/낙관적 모드**: 간단한 변환  
  
**전체 모드**: 빈 문자열 (0)  
  
**NULL 연결**  
이 설정은 문자열 연결을 NULL로 변환 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음과 같은 옵션을 설정할 수 있습니다.  
  
-   **ISNULL 함수를 사용 하 여 래핑:** 이 옵션을 설정 하면 연결에서 비상수 ' string_expression '가 모두 ISNULL (string_expression)으로 래핑되어 Null이 빈 문자열로 바뀝니다.  
  
-   **현재 구문 유지**  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** ISNULL 함수를 사용 하 여 래핑  
  
**빈 문자열 변환**  
이 설정은 빈 문자열을 변환 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음과 같은 옵션을 설정할 수 있습니다.  
  
-   **모든 문자열 식을 공백으로 바꿉니다.**  
  
-   **빈 문자열 상수를 공백으로 바꾸기**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** 모든 문자열 식을 공백으로 바꿉니다.  
  
**이진 문자열 변환 변환 및 캐스트**  
이진 값을 숫자로 변환 하는 경우 다른 플랫폼에서 다른 값을 반환할 수 있습니다. 예를 들어 x86 프로세서에서 CONVERT (integer, 0x00000100)는 ASE 및 256에서 65536을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 또한 ASE는 바이트 순서에 따라 다른 값을 반환 합니다.  
  
이 설정을 사용 하 여 SSMA가 이진 값을 포함 하는 변환 및 CASE 식을 변환 하는 방법을 제어할 수 있습니다.  
  
-   경고 또는 수정 없이 식을 변환 하려면 **단순 변환** 을 선택 합니다. ASE 서버에 이진 값을 변경할 필요가 없는 바이트 순서가 있는 경우이 설정을 사용 합니다.  
  
-   **변환 및 수정** 을 선택 하 여 ssma에서 사용할 식을 변환 하 고 수정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 리터럴 상수의 바이트 순서가 반대로 바뀝니다. 다른 모든 이진 값 (예: 이진 변수 및 열)은 오류로 표시 됩니다. ASE 서버에 이진 값을 변경 해야 하는 바이트 순서가 있는 경우이 값을 사용 합니다.  
  
-   변환 **및 경고로 표시** 를 선택 하 여 ssma가 식을 변환 하 고 수정 하도록 한 다음 변환 된 모든 식을 경고 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본 모드:** 경고를 사용 하 여 변환 및 표시  
  
**낙관적 모드:** 간단한 변환  
  
**전체 모드:** 변환 및 수정  
  
**동적 SQL**  
이 설정을 사용 하 여 ASE 코드에서 동적 SQL을 발견할 때 SSMA에서 출력 또는 오류 목록 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.  
  
-   변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 동적 SQL을 변환 하 고 문을 경고 주석으로 표시 합니다.  
  
-   **표시를 오류로 표시**를 선택 하면 ssma는 변환을 건너뛰고 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 경고를 사용 하 여 변환 및 표시  
  
**전체 모드:** 오류로 표시  
  
**같음 확인 변환**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure에서는 ANSI_NULLS 설정이 on 인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같음 비교에 null 값이 포함 되어 있으면/SQL Azure UNKNOWN을 반환 합니다. ANSI_NULLS 해제 된 경우에는 비교 되는 열과 식 또는 두 식이 모두 null 이면 null 값을 포함 하는 같음 비교가 true를 반환 합니다. 기본적으로 (ANSINULL OFF) Sybase ASE 같음 비교는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS OFF를 사용 하는/SQL Azure와 동일 하 게 작동 합니다.  
  
-   **단순 변환**을 선택 하는 경우 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null 값에 대 한 추가 검사 없이 ASE 코드를/SQL Azure 구문으로 변환 합니다. /SQL Azure에서 ANSI_NULLS 꺼져 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있거나 case를 기준으로 같음 비교를 수정 하려는 경우이 설정을 사용 합니다.  
  
-   **Null 값 고려**를 선택 하는 경우 SSMA는 is NULL 및 IS not null 절을 사용 하 여 null 값에 대 한 검사를 추가 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 간단한 변환  
  
**전체 모드:** NULL 값 고려  
  
**서식 문자열**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure는 PRINT 및 RAISERROR 문의 *format_string* 인수를 더 이상 지원 하지 않습니다. *Format_string* 변수는 대체 가능 매개 변수를 문자열에 직접 넣고 런타임에 매개 변수를 대체 하는 것을 지원 합니다. 대신에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자열 리터럴 또는 변수를 사용 하 여 작성 된 문자열을 사용 하 여 전체 문자열이 필요 합니다. 자세한 내용은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 온라인 설명서의 "PRINT ()" 항목을 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
SSMA는 *format_string* 인수를 발견할 경우 변수를 사용 하 여 문자열 리터럴을 작성 하거나 새 변수를 만들고 해당 변수를 사용 하 여 문자열을 작성할 수 있습니다.  
  
-   PRINT 및 RAISERROR 함수에 문자열 리터럴을 사용 하려면 **새 문자열 만들기**를 선택 합니다.  
  
    이 모드에서 PRINT 또는 RAISERROR 문이 자리 표시자 및 지역 변수를 사용 하지 않는 경우 문은 변경 되지 않습니다. 2% 문자 (%%) 인쇄 문자열 리터럴의 1% 문자%로 변경 됩니다.  
  
    PRINT 또는 RAISERROR 문에서 다음 예제와 같이 자리 표시자와 하나 이상의 지역 변수를 사용 하는 경우:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA는 다음 구문으로 변환 합니다.  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    *Format_string* 다음 문에서와 같이 변수입니다.  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA는 간단한 문자열 변환을 수행할 수 없으며 새 변수를 만들어야 합니다.  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    **새 문자열 모드 만들기** 를 사용 하는 경우 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CONCAT_NULL_YIELDS_NULL 옵션이 OFF 라고 가정 합니다. 따라서 SSMA는 null 인수를 확인 하지 않습니다.  
  
-   SSMA에서 각 PRINT 및 RAISERROR 문에 대해 새 변수를 작성 하 게 한 다음 해당 변수를 문자열 값으로 사용 하려면 **새 변수 만들기**를 선택 합니다.  
  
    이 모드에서 PRINT 또는 RAISERROR 문이 자리 표시자 및 지역 변수를 사용 하지 않는 경우 SSMA는 모든 이중% 문자 (%%)를 대체 합니다. /SQL Azure 구문을 준수 하는 1% 문자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    PRINT 또는 RAISERROR 문에서 다음 예제와 같이 자리 표시자와 하나 이상의 지역 변수를 사용 하는 경우:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA는 다음 구문으로 변환 합니다.  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    *Format_string* 다음 문에서와 같이 변수입니다.  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA는 다음과 같이 새 변수를 만들고 각 인수에서 null 값을 확인 합니다.  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 새 문자열 만들기  
  
**전체 모드:** 새 변수 만들기  
  
**Timestamp 열에 명시적 값 삽입**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure는 타임 스탬프 열에 명시적 값을 삽입 하는 것을 지원 하지 않습니다.  
  
-   INSERT 문에서 timestamp 열을 제외 하려면 **열 제외**를 선택 합니다.  
  
-   Timestamp 열이 INSERT 문에 있을 때마다 오류 메시지를 인쇄 하려면 **오류 표시**를 선택 합니다. 이 모드에서는 INSERT 문이 변환 되지 않고 오류 주석으로 표시 됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 열 제외  
  
**전체 모드:** 오류로 표시  
  
**프로시저에 정의 된 임시 개체 저장**  
이 설정은 프로시저에 표시 되는 임시 개체 정의를 변환 하는 동안 원본 메타 데이터에 저장 해야 하는지 여부를 지정 합니다.  
  
-   메타 데이터에 저장 하려면 **예** 를 선택 합니다.  
  
-   개체를 저장 하지 않아도 되는 경우 **아니요** 를 선택 합니다.  
  
**기본/최적 모드:** 예로  
  
**전체 모드:** 아니요  
  
**프록시 테이블 변환**  
ASE 프록시 테이블이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 테이블로 변환 되는지 아니면 변환 되지 않고 코드에 오류 주석이 표시 되는지 여부를 지정 합니다.  
  
-   **변환** 을 선택 하 여 프록시 테이블을 일반 테이블로 변환 합니다.  
  
-   오류가 **있는 표시** 를 선택 하 여 프록시 테이블 코드를 오류 주석으로 표시 하기만 하면 됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 오류로 표시  
  
**RAISERROR 기준 메시지 번호**  
ASE 사용자 메시지는 각 데이터베이스에 저장 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]사용자 메시지는 중앙에서 저장 되며, **메시지** 카탈로그 뷰를 통해 사용할 수 있게 됩니다. 또한 ASE 사용자 메시지는 2만에서 시작 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지는 50001에서 시작 합니다.  
  
이 설정은 ASE 사용자 메시지 번호에 추가 하 여 사용자 메시지로 변환 하는 번호를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 에서 사용자 메시지를 사용 하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 값을 큰 값으로 변경 해야 할 수 있습니다. **sys.messages** 이는 변환 된 메시지 번호가 기존 메시지 번호와 충돌 하지 않도록 하기 위한 것입니다.  
  
다음 사항에 유의하세요.  
  
-   17000-19999 범위의 ASE 메시지는 sysmessages 시스템 테이블에서 가져온 것 이며 변환 되지 않습니다.  
  
-   RAISERROR 문에서 참조 되는 메시지 번호가 상수인 경우 SSMA는 상수에 기본 메시지 번호를 추가 하 여 새 사용자 메시지 번호를 확인 합니다.  
  
-   참조 되는 메시지 번호가 변수 또는 식인 경우 SSMA는 중간 지역 변수를 만듭니다.  
  
-   낙관적 모드에서 SSMA는 CONCAT_NULL_YIELDS_NULL 옵션이 off 인 것으로 가정 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 NULL 인수를 확인 하지 않습니다.  
  
-   전체 모드에서 SSMA는 null 인수를 확인 합니다.  
  
-   ERRORDATA *목록이* 있는 RAISERROR는 변환 되지 않습니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 30001  
  
**시스템 개체**  
이 설정을 사용 하 여 ASE 시스템 개체를 사용 하는 경우 SSMA에서 출력 또는 오류 목록 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.  
  
-   변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 참조를 시스템 개체로 변환 하 고 문을 경고 주석으로 표시 합니다.  
  
-   **표시를 오류로 표시**를 선택 하면 ssma는 시스템 개체에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 경고를 사용 하 여 변환 및 표시  
  
**전체 모드:** 오류로 표시  
  
**확인 되지 않은 식별자**  
이 설정을 사용 하 여 id를 확인할 수 없는 경우 SSMA에서 출력 또는 오류 목록 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.  
  
-   **변환 및 경고로 표시**를 선택 하는 경우 ssma는 확인 되지 않은 식별자에 대 한 참조를 변환 하려고 시도 하 고 문을 경고 주석으로 표시 합니다.  
  
-   **표시를 오류로 표시**를 선택 하면 ssma는 확인 되지 않은 식별자에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 경고를 사용 하 여 변환 및 표시  
  
**전체 모드:** 오류로 표시  
  
## <a name="system-function-options"></a>시스템 함수 옵션  
**CHARINDEX 함수**  
ASE에서 CHARINDEX는 모든 입력 식이 NULL 인 경우에만 NULL을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입력 식이 NULL 이면/SQL Azure에서 NULL을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. CHARINDEX 함수에 대 한 모든 호출은 Sybase ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름 2ss의 사용자 데이터베이스에서 만들어짐)에 따라 CHARINDEX_VARCHAR 또는 CHARINDEX_NVARCHAR 사용자 정의 함수에 대 한 호출로 대체 됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** Replace 함수  
  
**DATALENGTH 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DATALENGTH 함수에서 반환 하는 값은 값이 단일 공간이 면/SQL Azure와 ASE는 다릅니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure는 0을 반환 하 고 ASE는 1을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. DATALENGTH 함수에 대 한 모든 호출은 Sybase ASE 동작을 에뮬레이트하는 CASE 식으로 대체 됩니다.  
  
-   기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** Replace 함수  
  
**INDEX_COL 함수**  
ASE는 INDEX_COL 함수에 대 한 선택적 *user_id* 인수를 지원 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure에서는이 인수를 지원 하지 않습니다. *User_id* 인수를 사용 하는 경우이 함수를/SQL Azure 구문으로 변환할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. 코드에 *user_id* 인수가 포함 된 경우 ssma는 오류를 표시 합니다.  
  
-   INDEX_COL 발생 될 때마다 오류 메시지를 표시 하려면 **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.  
  
**기본/최적/전체 모드:** 오류로 표시  
  
**INDEX_COLORDER 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure에 INDEX_COLORDER 시스템 함수가 없습니다.  
  
-   ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. INDEX_COLORDER 함수에 대 한 모든 호출은 Sybase ASE 동작을 에뮬레이트하는 동일한 이름 INDEX_COLORDER (스키마 이름에 사용자 데이터베이스에서 만들어짐)가 있는 사용자 정의 함수에 대 한 호출로 대체 됩니다.  
  
-   INDEX_COLORDER 발생 될 때마다 오류 메시지를 인쇄 하려면 **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 오류로 표시  
  
**LEFT 및 RIGHT 함수**  
Sybase의 Left 및 Right 함수는 음수 길이 매개 변수에 대해 다르게 동작 합니다.  
  
-   ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 그러면 길이 매개 변수가 음수 값에 대해 null을 반환 하는 CASE 식으로 바뀝니다.  
  
-   SQL Server 동작을 사용 하려면 **현재 구문 유지** 를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** Replace 함수  
  
> [!NOTE]  
> 길이 매개 변수가 복소수 식이 아닌 리터럴 값 이면 길이 값은 항상 프로젝트 설정에 관계 없이 null로 바뀝니다.  
  
**NEXT_IDENTITY 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure에 NEXT_IDENTITY 시스템 함수가 없습니다.  
  
-   ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. NEXT_IDENTITY 함수에 대 한 모든 호출은 Sybase ASE 동작을 에뮬레이트하는 식 (IDENT_CURRENT (매개 변수 값) + IDENT_INCR (매개 변수 값)으로 대체 됩니다.  
  
-   NEXT_IDENTITY 발생 될 때마다 오류 메시지를 인쇄 하려면 **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 오류로 표시  
  
**PATINDEX 함수**  
PATINDEX 함수를 Sybase ASE 동작과 일치 하도록 변환할지 여부를 지정 합니다. Point는 Sybase가 검색 패턴에서 후행 공백을 잘라내는 것입니다. 해결 방법은 값 식을 최대 전체 자릿수로 고정 길이 데이터 형식으로 캐스팅 하 고 검색 패턴에 rtrim 함수를 적용 하는 것입니다.  
  
-   ASE 동작을 사용 하려면 **사용**을 선택 합니다.  
  
-   기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 동작을 사용 하려면 사용 안 **함**을 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 사용 안 함  
  
**전체 모드:** 사용  
  
**REPLICATE 함수**  
복제 함수는 문자열을 지정 된 횟수 만큼 반복 합니다. ASE에서 문자열을 0 회 반복 하도록 지정 하는 경우 결과는 null입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure에서는 빈 문자열이 반환 됩니다.  
  
-   ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 모든 복제 함수 호출은 Sybase ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름 2의 사용자 데이터베이스에서 만들어짐)에 따라 REPLICATE_VARCHAR 또는 REPLICATE_NVARCHAR 사용자 정의 함수에 대 한 호출로 대체 됩니다.  
  
-   기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 동작을 사용 하려면 **함수 바꾸기**를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드/전체 모드:** Replace 함수  
  
**TRIM (LTRIM, RTRIM) 함수**  
이 설정은 Trim (LTRIM, RTRIM) 함수에 대 한 호출을 Sybase ASE와 동등한 구문 함수로 바꿀지 아니면 현재 구문을 유지할지를 지정 합니다. 이 특정 설정에 대해 다음 옵션이 제공 됩니다.  
  
-   **Replace 함수**  
  
-   **현재 구문 유지**  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드/전체 모드:** Replace 함수  
  
**SUBSTRING 함수**  
ASE에서 함수는 `SUBSTRING(expression, start, length)` 식의 문자 수보다 큰 시작 값이 지정 된 경우 NULL을 반환 하 고, 길이가 0 이면 NULL을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure에서 해당 하는 식은 빈 문자열을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. SUBSTRING 함수에 대 한 모든 호출은 Sybase ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름에 사용자 데이터베이스에서 생성 됨)을 기반으로 하는 SUBSTRING_VARCHAR 또는 SUBSTRING_NVARCHAR 또는 SUBSTRING_VARBINARY 사용자 정의 함수에 대 한 호출로 대체 됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 현재 구문 유지  
  
**전체 모드:** Replace 함수  
  
## <a name="tables"></a>TABLES  
**기본 키 추가**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]액세스 테이블에 기본 키 또는 고유 인덱스가 없는 경우 또는 SQL Azure 테이블에 새 기본 키를 만듭니다.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
> [!NOTE]  
> SQL Azure에 연결 된 경우 기본적으로 True입니다.  
  
## <a name="see-also"></a>참고 항목  
[사용자 인터페이스 참조 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
