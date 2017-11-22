---
title: "프로젝트 설정 (변환) (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07ba161d9f053e35c80f9c22627a55a4f1cab003
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-conversion-sybasetosql"></a>프로젝트 설정 (변환) (SybaseToSQL)
변환 페이지는 **프로젝트 설정** 대화 상자 SSMA Sybase 적응형 Server Enterprise (ASE) 구문을 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문이 있습니다.  
  
변환에서 제공 되는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자:  
  
-   모든 SSMA 프로젝트에 대 한 설정을 지정 하려는 경우는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
## <a name="miscellaneous-options"></a>기타 옵션  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 및 ASE 다른 오류 코드를 사용 합니다.  
  
에 대 한 참조를 발견 한 경우 SSMA 출력이 나 오류 목록 창에 표시 된 메시지 (경고 또는 오류)의 형식을 지정 하려면이 설정을 사용 하 여 **@@ERROR**  ASE 코드에서입니다.  
  
-   선택 하는 경우 **변환 하 고 경고로 표시**, SSMA 문을 변환 되며 경고 주석으로 표시 합니다.  
  
-   선택 하는 경우 **오류로 표시**, SSMA를 건너뛰어 변환 오류 주석 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 변환 하 고 경고로 표시  
  
**전체 모드:** 오류로 표시  
  
**LIKE 연산자 변환**  
Sybase ASE 동작과 일치에 대 한 피연산자와 같은 변환할지 여부를 지정 합니다. 중요 한 점은 Sybase like 패턴에서 후행 공백을 삭제 합니다.는 것입니다. 해결 방법은 최대 전체 자릿수는 고정된 길이 데이터 형식에 오른쪽 식의 캐스트 하는 것입니다.  
  
-   선택 **단순 변환이** 모든 수정 하지 않고 식을 변환 합니다.  
  
-   ASE 동작 select를 사용 하려면 **고정된 길이 캐스팅 합니다.**  
  
모드 상자에서 변환 모드를 선택 하면 SSMA 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드**: 단순 변환  
  
**전체 모드**: 고정된 길이 캐스팅  
  
**변환 또는 빈 문자열을 숫자 형식 캐스팅**  
비어 있거나 공백 문자열 데이터 형식 인수로 숫자 형식과 CONVERT 또는 CAST 식 내에서 처리 하는 방법을 지정 합니다. 다음 옵션은이 설정에 대해 사용할 수 있습니다.  
  
-   선택 **단순 변환이** 모든 수정 하지 않고 식을 변환 합니다.  
  
-   경우 **비어 있는 0으로 숫자 문자열** 을 선택한 경우 사례 ltrim(rtrim({s})) 문자열 매개 변수 {s}을 대체할 때 "" 다음 0 else {s} END 식이  
  
모드 상자에서 변환 모드를 선택 하면 SSMA 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드**: 단순 변환  
  
**전체 모드**: 비어 있는 0으로 숫자 문자열  
  
**NULL의 연결**  
이 설정은 NULL 인 문자열 연결을 변환 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음 옵션을 설정할 수 있습니다.  
  
-   **ISNULL 함수로 래핑하:** 하는 경우이 옵션을 설정, 모든 상수가 아닌 연결에 사용 되는 ' string_expression' ISNULL(string_expression) 래핑 및 빈 문자열이 있는 null 값을 대체 됩니다.  
  
-   **현재 구문을 유지합니다**  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** ISNULL 함수로 줄 바꿈  
  
**빈 문자열 변환**  
이 설정은 빈 문자열을 변환 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음 옵션을 설정할 수 있습니다.  
  
-   **공간으로 모든 문자열 식 대체**  
  
-   **빈 문자열 상수 공간으로 대체**  
  
-   사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 동작 **현재 구문을 유지**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** 공간으로 모든 문자열 식 대체  
  
**변환 및 캐스트 이진 문자열 변환**  
이진 값의 숫자 변환 서로 다른 플랫폼에서 다른 값을 반환할 수 있습니다. 예를 들어 x86에 ASE에 65536 및에서 256 개 프로세서, CONVERT (정수, 0x00000100)를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 또한 ASE 바이트 순서에 따라 다른 값을 반환합니다.  
  
이 설정을 SSMA 변환으로 변환 하는 방법 및 이진 값이 포함 된 CASE 식 사용:  
  
-   선택 **단순 변환이** 경고 또는 수정 하지 않고 식을 변환 합니다. ASE 서버에는 이진 값의 변경 내용을 필요 하지 않은 바이트 순서를 알고 있는 경우이 설정을 사용 합니다.  
  
-   선택 **변환 하 고 해결** SSMA 변환 하 고 사용 하기 위해 식에서 해결 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 리터럴 상수에 바이트 순서 반대로 바뀝니다. 다른 모든 이진 값 (예: 이진 변수 및 열)는 오류와 함께 표시 됩니다. ASE 서버에 이진 값을 변경 해야 하는 바이트 순서를 알고 있는 경우이 값을 사용 합니다.  
  
-   선택 **변환 하 고 경고로 표시** SSMA 변환 및 식, 해결 하 고 모든 있어야 경고 주석 사용 하 여 식을 변환 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본 모드:** 변환 하 고 경고로 표시  
  
**최적 모드:** 간단한 변환  
  
**전체 모드:** 변환 하 고 해결  
  
**동적 SQL**  
SSMA ASE 코드에서 동적 SQL에 도달할 때 출력이 나 오류 목록 창에 표시 된 메시지 (경고 또는 오류)의 형식을 지정 하려면이 설정을 사용 합니다.  
  
-   선택 하는 경우 **변환 하 고 경고로 표시**, SSMA는 동적 SQL을 변환 하 고 경고 주석 사용 하 여 문을 표시 합니다.  
  
-   선택 하는 경우 **오류로 표시**, SSMA를 건너뛰어 변환 오류 주석 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 변환 하 고 경고로 표시  
  
**전체 모드:** 오류로 표시  
  
**같음 확인 변환**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 ANSI_NULLS 설정 켜져 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 같음 비교는 null 값을 포함 하는 경우 UNKNOWN을 반환 합니다. ANSI_NULLS off 이면 null 값을 포함 하는 같음 비교 경우 true를 반환 비교 된 열 및 식 또는 두 식이 모두 null입니다. (ANSINULL OFF) 기본 Sybase ASE 같음으로 비교 처럼 동작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure로 ANSI_NULLS OFF입니다.  
  
-   선택 하는 경우 **단순 변환이**, SSMA는 ASE 코드를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ null 값에 대 한 추가 검사 하지 않고 SQL Azure 구문입니다. ANSI_NULLS 옵션이 off의 경우이 설정을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 또는 사례 당 기준 같음 비교를 수정 하려는 경우.  
  
-   선택 하는 경우 **NULL 고려 값**, SSMA IS NULL 및 IS NOT NULL 절을 사용 하 여 null 값에 대 한 검사를 추가 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 간단한 변환  
  
**전체 모드:** 고려 NULL 값  
  
**형식 문자열**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 더 이상 지원는 *format_string* PRINT 및 RAISERROR 문의의 인수입니다. *format_string* 변수 지원 되는 대체 가능 매개 변수는 문자열에 직접 배치 및 다음 실행 시 매개 변수를 대체 합니다. 대신, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변수를 사용 하 여 작성 하는 문자열 또는 문자열 리터럴을 사용 하 여 전체 문자열이 필요 합니다. 자세한 내용은 참조는 "인쇄 ([!INCLUDE[tsql](../../includes/tsql_md.md)])" 항목을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
SSMA 발생 했을 때는 *format_string* 인수를 해당 변수를 사용 하 여 리터럴 문자열을 작성할 또는 새 변수 만들고 해당 변수를 사용 하 여 문자열을 작성 합니다.  
  
-   PRINT 및 RAISERROR 함수에 대 한 리터럴 문자열을 사용 하려면 선택 **새 문자열을 만들**합니다.  
  
    이 모드에서 자리 표시자 및 지역 변수는 PRINT 또는 RAISERROR 문을 사용 하지 않는 경우 문을 변경 되지 않습니다. 이중 백분율 문자 (%)은 인쇄 문자열 리터럴에서 단일 백분율 문자 %로 변경 됩니다.  
  
    자리 표시자와 PRINT 또는 RAISERROR 문을 사용 하는 경우 또는 다음 예제와 같이 더 많은 지역 변수:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 다음 구문으로 변환 됩니다.  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    경우 *format_string* 다음 문에서 변수와 같은:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA는 간단한 문자열 변환을 수행할 수 없습니다 및 새 변수를 만들어야 합니다.  
  
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
    사용 하는 경우 **새 문자열을 만들** 모드에서는 SSMA 가정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 옵션 CONCAT_NULL_YIELDS_NULL이 OFF입니다. 따라서 SSMA null 인수를 확인 하지 않습니다.  
  
-   SSMA 각 PRINT 및 RAISERROR 문에 대 한 새 변수를 빌드하고 다음 문자열 값에 대 한 변수를 사용 하도록 선택 **새 변수 만들기**합니다.  
  
    이 모드에서는 자리 표시자 및 지역 변수는 PRINT 또는 RAISERROR 문을 사용 하지 않는 경우 SSMA 모든 이중 백분율 문자 (%)으로 대체 충족 하기 위해 단일 백분율 문자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 구문입니다.  
  
    자리 표시자와 PRINT 또는 RAISERROR 문을 사용 하는 경우 또는 다음 예제와 같이 더 많은 지역 변수:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 다음 구문으로 변환 됩니다.  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    경우 *format_string* 다음 문에서 변수와 같은:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 새 변수를 만듭니다 다음과 같이 각 인수에 null 값을 확인 합니다.  
  
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
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 새 문자열 만들기  
  
**전체 모드:** 새 변수 만들기  
  
**타임 스탬프 열에 명시적인 값을 삽입 합니다.**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 타임 스탬프 열에 명시적 값을 삽입 하는 것을 지원 하지 않습니다.  
  
-   를 INSERT 문을에서 타임 스탬프 열을 제외 하려면 선택 **제외 열**합니다.  
  
-   오류 메시지를 인쇄 하는 INSERT 문에서 타임 스탬프 열이 될 때마다 선택 **오류로 표시**합니다. 이 모드에서는 INSERT 문을 변환 되지 않습니다 및 오류 주석으로 표시 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 제외 열  
  
**전체 모드:** 오류로 표시  
  
**저장 프로시저에 정의 된 임시 개체**  
이 설정은 절차에 표시 되는 임시 개체 정의 변환 하는 동안 원본 메타 데이터에 저장 해야 하는 경우를 지정 합니다.  
  
-   선택 **예** 메타 데이터에 저장할 수 있습니다.  
  
-   선택 **아니요** 개체를 저장할 수 있어야 하는 경우.  
  
**기본/낙관적 모드:** 예  
  
**전체 모드:** 아니요  
  
**프록시 테이블 변환**  
ASE 프록시 테이블을 변환 하는 경우 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 테이블, 또는 변환 되지 및 코드 오류 주석으로 표시 됩니다.  
  
-   선택 **변환** 프록시 테이블을 일반 테이블과 변환할 수 있습니다.  
  
-   선택 **오류로 표시** 단순히 오류 주석 사용 하 여 프록시 테이블 코드를 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** 오류로 표시  
  
**RAISERROR 기본 메시지 번호**  
ASE 사용자 메시지는 각 데이터베이스에 저장 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]사용자 메시지 중앙 집중식으로 저장 되 고를 통해 사용할 수는 **sys.messages** 카탈로그 뷰에 있습니다. ASE 사용자 메시지 20000에서 뿐만 아니라 시작 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 오류 메시지 50001에서 시작 합니다.  
  
이 설정은 지정 변환할 ASE 사용자 메시지 번호에 추가할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용자 메시지입니다. 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용자 메시지에는 **sys.messages** 카탈로그 뷰를 큰 값으로이 번호를 변경 해야 할 수 있습니다. 되므로 변환 된 메시지 번호 기존 메시지 번호와 충돌 하지 않습니다.  
  
다음에 유의하세요.  
  
-   17000 19999 범위의 ASE 메시지 sysmessages 시스템 테이블에서 되며 변환 되지 않습니다.  
  
-   RAISERROR 문을에서 참조 되는 메시지 번호 상수 이면 SSMA 새 사용자 메시지 수를 확인 하는 상수에는 기본 메시지 번호를 추가 합니다.  
  
-   참조 되는 메시지 번호는 변수 또는 식 이면 SSMA 중간 로컬 변수를 만들어집니다.  
  
-   SSMA 가정 하는 최적 모드에서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 옵션 CONCAT_NULL_YIELDS_NULL이 off 인 해지고 null 인수를 검사 하지 않습니다.  
  
-   전체 모드로 SSMA null 인수를 확인합니다.  
  
-   RAISERROR와 error-데이터 *목록* 변환 되지 않습니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 30001  
  
**시스템 개체**  
SSMA ASE 시스템 개체의 사용에 도달할 때 출력이 나 오류 목록 창에 표시 된 메시지 (경고 또는 오류)의 형식을 지정 하려면이 설정을 사용 합니다.  
  
-   선택 하는 경우 **변환 하 고 경고로 표시**, SSMA는 시스템 개체에 대 한 참조를 변환 및 경고 주석 사용 하 여 문을 표시 합니다.  
  
-   선택 하는 경우 **오류로 표시**, SSMA는 시스템 개체에 대 한 참조를 변환 하지 않습니다 및 오류 주석 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 변환 하 고 경고로 표시  
  
**전체 모드:** 오류로 표시  
  
**확인 되지 않은 식별자**  
SSMA는 식별자를 확인할 수 없는 경우 출력이 나 오류 목록 창에 표시 된 메시지 (경고 또는 오류)의 형식을 지정 하려면이 설정을 사용 합니다.  
  
-   선택 하는 경우 **변환 하 고 경고로 표시**, SSMA 확인 되지 않은 식별자에 대 한 참조를 변환 하 려 하 고 경고 주석 사용 하 여 문을 표시 합니다.  
  
-   선택 하는 경우 **오류로 표시**, SSMA는 확인 되지 않은 식별자에 대 한 참조를 변환 하지 않습니다 및 오류 주석 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 변환 하 고 경고로 표시  
  
**전체 모드:** 오류로 표시  
  
## <a name="system-function-options"></a>시스템 함수 옵션  
**CHARINDEX 함수**  
ASE, CHARINDEX 모든 입력된 식은 null 일 경우에 NULL을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 입력된 식이 NULL 이면 NULL을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 선택 **Replace 함수**합니다. CHARINDEX 함수에 대 한 모든 호출 (만든 사용자 데이터베이스의 스키마 이름 's2ss' 아래) Sybase ASE 동작을 에뮬레이션 하려면 전달 된 매개 변수의 형식에 따라 CHARINDEX_VARCHAR 또는 CHARINDEX_NVARCHAR 사용자 정의 함수를 호출 하 여 대체 됩니다.  
  
-   사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 동작 **현재 구문을 유지**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** Replace 함수  
  
**DATALENGTH 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ 값이 공백 하나로 DATALENGTH 함수에서 반환한 값 SQL Azure 및 ASE 다릅니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ 0을 반환 하는 SQL Azure 및 ASE 1을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 선택 **Replace 함수**합니다. DATALENGTH 함수에 대 한 모든 호출을 Sybase ASE 동작을 에뮬레이션 하기 위해 CASE 식을 사용 하 여 대체 됩니다.  
  
-   기본값을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / SQL Azure 동작 **현재 구문을 유지**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** Replace 함수  
  
**INDEX_COL 함수**  
그러나 ASE 지원 선택적 *user_id* INDEX_COL 함수; 인수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는이 인수를 지원 하지 않습니다. 사용 하는 경우는 *user_id* 인수를이 함수는로 변환할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 구문입니다.  
  
-   ASE 동작을 사용 하려면 선택 **함수 변환**합니다. 코드를 포함 하는 경우는 *user_id* 인수를 SSMA 오류가 표시 됩니다.  
  
-   오류 메시지가 발생할 때마다 해당 INDEX_COL을 표시 하려면 선택 **오류로 표시**합니다. SSMA는 함수에 대 한 참조를 변환 되지 않습니다 및 오류 설명 사용 하 여 문을 표시 합니다.  
  
**기본/Optimistic/전체 모드:** 오류로 표시  
  
**INDEX_COLORDER 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 INDEX_COLORDER 시스템 함수는 없습니다.  
  
-   ASE 동작을 사용 하려면 선택 **함수 변환**합니다. INDEX_COLORDER 함수에 대 한 모든 호출 INDEX_COLORDER (스키마 이름 's2ss'에서 사용자 데이터베이스에 생성 됨)는 Sybase ASE 동작을 에뮬레이트하는 같은 이름의 사용자 정의 함수에 대 한 호출으로 대체 됩니다.  
  
-   오류 메시지가 발생할 때마다 해당 INDEX_COLORDER를 인쇄 하려면 선택 **오류로 표시**합니다. SSMA는 함수에 대 한 참조를 변환 되지 않습니다 및 오류 설명 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** 오류로 표시  
  
**왼쪽 및 오른쪽 함수**  
왼쪽 및 오른쪽 함수 Sybase에 음수 길이 매개 변수에 대 한 다르게 동작합니다.  
  
-   ASE 동작을 사용 하려면 선택 **Replace 함수**합니다. 길이 매개 변수가 음수 값에 대해 null을 반환 하는 경우 식으로 대체 됩니다.  
  
-   SQL Server 동작을 사용 하려면 선택 **현재 구문을 유지**  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** Replace 함수  
  
> [!NOTE]  
> 길이 매개 변수는 리터럴 값 이며 not 복잡 한 식은 경우 length 값은 항상 프로젝트 설정에 관계 없이 null 바뀝니다.  
  
**NEXT_IDENTITY 함수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 NEXT_IDENTITY 시스템 함수는 없습니다.  
  
-   ASE 동작을 사용 하려면 선택 **함수 변환**합니다. NEXT_IDENTITY 함수에 대 한 모든 호출 (IDENT_CURRENT(parameter Value) + Sybase ASE 동작을 에뮬레이트하는 IDENT_INCR(parameter Value) 식으로 대체 됩니다.  
  
-   오류 메시지가 발생할 때마다 해당 NEXT_IDENTITY를 인쇄 하려면 선택 **오류로 표시**합니다. SSMA는 함수에 대 한 참조를 변환 되지 않습니다 및 오류 설명 사용 하 여 문을 표시 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** 오류로 표시  
  
**PATINDEX 함수**  
PATINDEX 함수 Sybase ASE 동작과 일치를 변환할지 여부를 지정 합니다. 중요 한 점은 Sybase 검색 패턴에서 후행 공백을 삭제 합니다.는 것입니다. 고정된 길이 데이터 형식의 최대 전체 자릿수 및 패턴을 검색 하려면 rtrim 함수를 적용 하는 값 식의 캐스트이 문제를 해결 합니다.  
  
-   ASE 동작 select를 사용 하려면 **사용**합니다.  
  
-   기본값을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 동작 **사용 하지 않는**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 사용 하지 않습니다  
  
**전체 모드:** 사용  
  
**REPLICATE 함수**  
REPLICATE 함수는 문자열의 지정 된 횟수 만큼 반복합니다. ASE에서 문자열에 0 번 반복 하도록 지정 하면 결과 null입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 결과 빈 문자열입니다.  
  
-   ASE 동작을 사용 하려면 선택 **Replace 함수**합니다. REPLICATE 함수에 대 한 모든 호출 (만든 사용자 데이터베이스의 스키마 이름 's2ss' 아래) Sybase ASE 동작을 에뮬레이션 하려면 전달 된 매개 변수의 형식에 따라 REPLICATE_VARCHAR 또는 REPLICATE_NVARCHAR 사용자 정의 함수를 호출 하 여 대체 됩니다.  
  
-   기본값을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 동작 **Replace 함수**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드/전체 모드:** Replace 함수  
  
**TRIM (LTRIM, RTRIM) 함수**  
이 설정은 Sybase ASE에 해당 하는 구문 함수 (LTRIM, RTRIM) Trim 함수 호출을 대체 하거나 현재 구문 유지할 수 여부를 지정 합니다. 다음 옵션은이 특정 한 설정에 대 한.  
  
-   **Replace 함수**  
  
-   **현재 구문을 유지합니다**  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드/전체 모드:** Replace 함수  
  
**SUBSTRING 함수**  
ASE를 함수에 `SUBSTRING(expression, start, length)` 길이 0과 같을 경우 또는 식의 문자 수보다 큰 시작 값을 지정 하는 경우 NULL을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure는 식은 빈 문자열을 반환 합니다.  
  
-   ASE 동작을 사용 하려면 선택 **Replace 함수**합니다. SUBSTRING 함수에 대 한 모든 호출 (만든 사용자 데이터베이스의 스키마 이름 's2ss' 아래) Sybase ASE 동작을 에뮬레이션 하려면 전달 된 매개 변수의 형식에 따라 SUBSTRING_VARCHAR 또는 SUBSTRING_NVARCHAR SUBSTRING_VARBINARY 사용자 정의 함수를 호출 하 여 대체 됩니다.  
  
-   사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / SQL Azure 동작 **현재 구문을 유지**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 현재 구문을 유지  
  
**전체 모드:** Replace 함수  
  
## <a name="tables"></a>TABLES  
**기본 키를 추가 합니다.**  
새 기본 키를 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Access 테이블에 기본 키 또는 고유 인덱스 일 경우 SQL Azure 테이블입니다.  
  
-   **기본 모드**: False  
  
-   **최적 모드**: False  
  
-   **전체 모드**: True  
  
> [!NOTE]  
> SQL Azure에 연결 되어 있을 때 True 기본적입니다.  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 참조 &#40; SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
