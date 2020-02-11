---
title: DB2 스키마 변환 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7a16a28a163acece321cc2229e9988cf7ab01f9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989871"
---
# <a name="converting-db2-schemas-db2tosql"></a>DB2 스키마 변환 (DB2ToSQL)
DB2에 연결 하 고,에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 하 고, 프로젝트 및 데이터 매핑 옵션을 설정한 후 db2 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체로 변환할 수 있습니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
데이터베이스 개체를 변환 하면 d b 2의 개체 정의를 사용 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 여 유사한 개체로 변환한 다음이 정보를 ssma 메타 데이터로 로드 합니다. 인스턴스에 정보를 로드 하지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 그런 다음 메타 데이터 탐색기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 개체 및 해당 속성을 볼 수 있습니다.  
  
변환 하는 동안 SSMA는 출력 창에 출력 메시지를 인쇄 하 고 오류 목록 창에 오류 메시지를 출력 합니다. 출력 및 오류 정보를 사용 하 여 원하는 변환 결과를 얻기 위해 DB2 데이터베이스 또는 변환 프로세스를 수정 해야 하는지 여부를 결정할 수 있습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 변환 옵션을 검토 합니다. 이 대화 상자를 사용 하 여 SSMA에서 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)을 참조 하세요.  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서는 변환 된 DB2 개체 및 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 보여 줍니다.  
  
|DB2 개체|결과 SQL Server 개체|  
|-----------|----------------------------|  
|데이터 형식|**SSMA는 아래에 나열 된 다음을 제외한 모든 유형을 매핑합니다.**<br /><br />CLOB:이 형식의 작업에 대 한 일부 네이티브 함수는 지원 되지 않습니다 (예: CLOB_EMPTY ()).<br /><br />BLOB:이 형식의 작업에 대 한 일부 네이티브 함수는 지원 되지 않습니다 (예: BLOB_EMPTY ()).<br /><br />DBLOB:이 형식의 작업에 대 한 일부 네이티브 함수는 지원 되지 않습니다 (예: DBLOB_EMPTY ()).|  
|사용자 정의 형식|**SSMA는 다음 사용자 정의를 매핑합니다.**<br /><br />고유 형식<br /><br />구조화 된 형식<br /><br />SQL PL 데이터 형식-참고: Weak 커서 유형이 지원 되지 않습니다.|  
|특수 레지스터|**SSMA는 아래에 나열 된 레지스터를 매핑합니다.**<br /><br />현재 타임 스탬프<br /><br />현재 날짜<br /><br />현재 시간<br /><br />현재 표준 시간대<br /><br />현재 사용자<br /><br />SESSION_USER 및 사용자<br /><br />SYSTEM_USER<br /><br />현재 CLIENT_APPLNAME<br /><br />현재 CLIENT_WRKSTNNAME<br /><br />현재 잠금 제한 시간<br /><br />현재 스키마<br /><br />현재 서버<br /><br />현재 격리<br /><br />기타 특수 레지스터는 SQL server 의미 체계에 매핑되지 않습니다.|  
|CREATE TABLE|**SSMA 맵은 다음과 같은 예외를 CREATE TABLE 합니다.**<br /><br />MDC (Multidimensional 클러스터링) 테이블<br /><br />범위 클러스터형 테이블 (.RCT)<br /><br />분할된 테이블<br /><br />분리 된 테이블<br /><br />데이터 캡처 절<br /><br />암시적으로 숨겨진 옵션<br /><br />VOLATILE 옵션|  
|CREATE VIEW|SSMA 맵은 ' WITH LOCAL CHECK OPTION '이 포함 된 뷰를 만들지만 다른 옵션은 SQL server 의미 체계에 매핑되지 않습니다.|  
|CREATE  INDEX|**SSMA 맵은 다음과 같은 예외를 사용 하 여 인덱스를 만듭니다.**<br /><br />XML 인덱스<br /><br />겹치지 않는 BUSINESS_TIME 옵션<br /><br />분할 된 절<br /><br />SPECIFICATION ONLY 옵션<br /><br />옵션을 사용 하 여 확장<br /><br />MINPCTUSED 옵션<br /><br />페이지 분할 옵션|  
|트리거|**SSMA는 다음과 같은 트리거 의미 체계를 매핑합니다.**<br /><br />각 행 트리거의 이후/<br /><br />/FOR 각 문이 트리거되는 경우<br /><br />각 행에 대 한/또는 각 행 트리거의 INSTEAD OF/for|  
|시퀀스|매핑됩니다.|  
|SELECT 문|**SSMA 맵은 다음 예외를 제외 하 고 선택 합니다.**<br /><br />데이터 변경-테이블 참조 절-부분적으로 매핑 되었지만 최종 테이블이 지원 되지 않음<br /><br />테이블 참조 절-부분적으로 매핑 되었지만-테이블 참조, 외부 테이블 참조, analyze_table 식, 컬렉션 파생 테이블, xmltable 식이 SQL server 의미 체계에 매핑되지 않습니다.<br /><br />기간-사양 절-매핑되지 않음<br /><br />Continue-handler 절-매핑되지 않았습니다.<br /><br />형식화 된 상관 관계 절-매핑되지 않았습니다.<br /><br />동시 액세스 확인 절-매핑되지 않았습니다.|  
|VALUES 문|가 매핑됩니다.|  
|INSERT 문|가 매핑됩니다.|  
|UPDATE 문|S**SMA 맵은 다음 예외를 제외 하 고 업데이트 합니다.**<br /><br />테이블 참조 절 전용-테이블 참조가 SQL server 의미 체계에 매핑되지 않습니다.<br /><br />Period 절이 매핑되지 않았습니다.|  
|MERGE 문|**SSMA 맵은 다음 예외와 병합 됩니다.**<br /><br />각 절의 단일 vs 여러 항목-각 절의 제한 된 발생에 대 한 SQL server 의미 체계에 매핑됩니다.<br /><br />SIGNAL 절-SQL Server 의미 체계에 매핑되지 않습니다.<br /><br />Mixed UPDATE 및 DELETE 절-SQL Server 의미 체계에 매핑되지 않습니다.<br /><br />Period-절-SQL Server 의미 체계에 매핑되지 않습니다.|  
|DELETE 문|**SSMA 맵은 다음 예외를 제외 하 고 삭제 합니다.**<br /><br />테이블 참조 절 전용-테이블 참조가 SQL server 의미 체계에 매핑되지 않습니다.<br /><br />Period 절-SQL Server 의미 체계에 매핑되지 않습니다.|  
|격리 수준 및 잠금 유형|가 매핑됩니다.|  
|프로시저 (SQL)|매핑됩니다.|  
|프로시저 (외부)|수동 업데이트가 필요 합니다.|  
|프로시저 (원본)|SQL Server 의미 체계에 매핑하지 않습니다.|  
|대입문|가 매핑됩니다.|  
|프로시저에 대 한 CALL 문|가 매핑됩니다.|  
|CASE 문|가 매핑됩니다.|  
|FOR 문|가 매핑됩니다.|  
|GOTO 문|가 매핑됩니다.|  
|IF 문|가 매핑됩니다.|  
|반복 문|가 매핑됩니다.|  
|LEAVE 문|가 매핑됩니다.|  
|LOOP 문|가 매핑됩니다.|  
|REPEAT 문|가 매핑됩니다.|  
|RESIGNAL 문|조건이 지원 되지 않습니다. 메시지는 선택 사항이 될 수 있습니다.|  
|RETURN 문|가 매핑됩니다.|  
|SIGNAL 문|조건이 지원 되지 않습니다. 메시지는 선택 사항이 될 수 있습니다.|  
|WHILE 문|가 매핑됩니다.|  
|진단 문 가져오기|**SSMA 맵은 다음과 같은 예외를 사용 하 여 진단을 가져옵니다.**<br /><br />ROW_COUNT-매핑됩니다.<br /><br />DB2_RETURN_STATUS-매핑됩니다.<br /><br />MESSAGE_TEXT-매핑됩니다.<br /><br />DB2_SQL_NESTING_LEVEL-SQL Server 의미 체계에 매핑되지 않습니다.<br /><br />DB2_TOKEN_STRING-SQL Server 의미 체계에 매핑되지 않습니다.|  
|커서|**SSMA는 다음과 같은 예외를 제외 하 고 커서를 매핑합니다.**<br /><br />CURSOR 문 할당-SQL Server 의미 체계에 매핑되지 않습니다.<br /><br />LOCATOR 문의 연결-SQL Server 의미 체계에 매핑되지 않습니다.<br /><br />DECLARE CURSOR 문-Returnability 절은 SQL server 의미 체계에 매핑되지 않습니다.<br /><br />FETCH 문-부분 매핑 변수는 target 으로만 지원 됩니다. SQLVAR 설명자가 SQL server 의미 체계에 매핑되지 않았습니다.|  
|variables|매핑됩니다.|  
|예외, 처리기 및 조건|**SSMA는 다음과 같은 예외를 제외 하 고 "예외 처리"를 매핑합니다.**<br /><br />종료 처리기-가 매핑됩니다.<br /><br />실행 취소 처리기-가 매핑됩니다.<br /><br />CONTINUE 처리기-매핑되지 않습니다.<br /><br />조건-SQL server 의미 체계에 매핑되지 않습니다.|  
|동적 SQL|매핑되지 않았습니다.|  
|별칭|매핑됩니다.|  
|애칭|부분 매핑 기본 개체에는 수동 처리가 필요 합니다.|  
|동의어|매핑됩니다.|  
|DB2의 표준 함수|SSMA 맵 DB2 표준 함수는 SQL Server에서 사용할 수 있는 경우에 해당 합니다.|  
|권한 부여|매핑되지 않았습니다.|  
|조건자|매핑됩니다.|  
|SELECT INTO 문|매핑되지 않았습니다.|  
|VALUES INTO 문|매핑되지 않았습니다.|  
|트랜잭션 제어|매핑되지 않았습니다.|  
  
## <a name="converting-db2-database-objects"></a>DB2 데이터베이스 개체 변환  
DB2 데이터베이스 개체를 변환 하려면 먼저 변환할 개체를 선택 하 고 SSMA에서 변환을 수행 하도록 합니다. 변환 하는 동안 출력 메시지를 보려면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**DB2 개체를 SQL Server 구문으로 변환 하려면**  
  
1.  DB2 메타 데이터 탐색기에서 DB2 서버를 확장 한 다음 **스키마**를 확장 합니다.  
  
2.  변환할 개체 선택:  
  
    -   모든 스키마를 변환 하려면 **스키마**옆의 확인란을 선택 합니다.  
  
    -   데이터베이스를 변환 하거나 생략 하려면 스키마 이름 옆의 확인란을 선택 합니다.  
  
    -   개체의 범주를 변환 하거나 생략 하려면 스키마를 확장 한 다음 범주 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 개체를 변환 하거나 생략 하려면 category 폴더를 확장 한 다음 개체 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 **스키마** 를 마우스 오른쪽 단추로 클릭 하 고 **스키마 변환**을 선택 합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **스키마 변환**을 선택 하 여 개별 개체 또는 개체 범주를 변환할 수도 있습니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 DB2 개체는 변환 되지 않을 수 있습니다. 요약 변환 보고서를 보면 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  DB2 메타 데이터 탐색기에서 **스키마**를 선택 합니다.  
  
2.  오른쪽 창에서 **보고서** 탭을 선택 합니다.  
  
    이 보고서는 평가 또는 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 DB2 메타 데이터 탐색기에서 스키마를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 DB2 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 있는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환이 실패 한 개체의 경우 변환 실패를 일으킨 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  DB2 메타 데이터 탐색기에서 **스키마**를 확장 합니다.  
  
2.  빨간색 오류 아이콘을 표시 하는 스키마를 확장 합니다.  
  
3.  스키마 아래에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
5.  오른쪽 창에서 **보고서** 탭을 클릭 합니다.  
  
6.  **보고서** 탭의 맨 위에는 드롭다운 목록이 있습니다. 목록에 **통계가**표시 되 면 선택 항목을 **원본**으로 변경 합니다.  
  
    SSMA는 소스 코드와 코드 바로 위에 몇 개의 단추를 표시 합니다.  
  
7.  **다음 문제** 단추를 클릭 합니다. 오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 발견 된 첫 번째 문제 소스 코드를 강조 표시 합니다.  
  
변환할 수 없는 각 항목에 대해 해당 개체를 사용 하 여 수행할 작업을 결정 해야 합니다.  
  
-   **SQL** 탭에서 프로시저에 대 한 소스 코드를 수정할 수 있습니다.  
  
-   DB2 데이터베이스의 개체를 수정 하 여 문제 코드를 제거 하거나 수정할 수 있습니다. 업데이트 된 코드를 SSMA에 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [DB2 데이터베이스에 연결 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)을 참조 하세요.  
  
-   마이그레이션할 때 개체를 제외할 수 있습니다. 메타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 탐색기 및 Db2 메타 데이터 탐색기에서 개체를 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 db2의 데이터를 마이그레이션하기 전에 항목 옆에 있는 확인란의 선택을 취소 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [변환 된 개체를 SQL Server 로드](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2 데이터를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
