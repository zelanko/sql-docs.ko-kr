---
title: DB2 스키마 (DB2ToSQL) 변환 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d509ad58491bca379e3ab86e07aee63e8a5d3946
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52520675"
---
# <a name="converting-db2-schemas-db2tosql"></a>DB2 스키마 (DB2ToSQL) 변환
DB2를 연결한 후에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 프로젝트 설정 및 데이터 매핑 옵션을 DB2 데이터베이스 개체를 변환할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체입니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
DB2에서 개체 정의 데이터베이스 개체 변환, 유사한로 변환한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 및 SSMA 메타 데이터에이 정보를 로드 합니다. 인스턴스로 정보를 로드 하지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용 하 여 개체 및 해당 속성을 보려면 다음을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기입니다.  
  
변환 중 SSMA 출력 창에 출력 메시지 및 오류 목록 창에 오류 메시지를 인쇄합니다. 출력 및 오류 정보를 사용 하 여 DB2 데이터베이스 또는 원하는 변환 결과 얻으려면 변환 프로세스를 수정 해야 하는지 여부를 결정 합니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 프로젝트 변환 옵션을 검토 합니다 **프로젝트 설정** 대화 상자. 이 대화 상자를 사용 하 여 SSMA 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)합니다.  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서 DB2 개체가 변환 되 고 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체:  
  
|DB2 개체|결과 SQL Server 개체|  
|-----------|----------------------------|  
|데이터 형식|**SSMA는 아래에 나열 된 다음을 제외한 모든 형식을 매핑합니다.**<br /><br />CLOB: 이 형식 사용 하 여 작업에 대 한 일부 기본 함수는 없습니다 (예: CLOB_EMPTY()) 지원<br /><br />BLOB: 이 형식 사용 하 여 작업에 대 한 일부 기본 함수는 없습니다 (예: BLOB_EMPTY()) 지원<br /><br />DBLOB: 이 형식 사용 하 여 작업에 대 한 일부 기본 함수는 없습니다 (예: DBLOB_EMPTY()) 지원|  
|사용자 정의 형식|**SSMA 매핑됩니다 다음 사용자 정의:**<br /><br />고유한 형식<br /><br />구조적된 형식<br /><br />SQL PL 데이터 형식-참고: 약한 커서 유형이 지원 되지 않습니다.|  
|특수 레지스터|**SSMA는 아래에 나열 된 레지스터를 매핑합니다.**<br /><br />현재 타임 스탬프<br /><br />현재 날짜<br /><br />현재 시간<br /><br />현재 표준 시간대<br /><br />현재 사용자<br /><br />SESSION_USER와 사용자<br /><br />SYSTEM_USER<br /><br />현재 CLIENT_APPLNAME<br /><br />현재 CLIENT_WRKSTNNAME<br /><br />현재 잠금 제한 시간<br /><br />현재 스키마<br /><br />현재 서버<br /><br />현재 격리<br /><br />다른 특별 한 등록는 SQL server 의미 체계에 매핑되지 않습니다.|  
|CREATE TABLE|**SSMA는 다음과 같은 예외를 사용 하 여 CREATE TABLE을 매핑합니다.**<br /><br />다차원 클러스터링 (MDC) 테이블<br /><br />범위 비클러스터형 테이블 (RCT)<br /><br />분할된 테이블<br /><br />분리 된 테이블<br /><br />데이터 캡처 절<br /><br />IMPLICITLY 숨겨진 옵션<br /><br />VOLATILE 옵션|  
|CREATE VIEW|SSMA ' WITH 로컬 CHECK OPTION으로 ' CREATE VIEW 매핑하지만 다른 옵션은 SQL server 의미 체계에 매핑되지 않은|  
|CREATE  INDEX|**SSMA는 다음과 같은 예외를 사용 하 여 CREATE INDEX를 매핑합니다.**<br /><br />XML 인덱스<br /><br />겹치는 없이 BUSINESS_TIME 옵션<br /><br />분할 된 절<br /><br />사양만 옵션<br /><br />확장 사용 하 여 옵션<br /><br />MINPCTUSED 옵션<br /><br />페이지 나누기 옵션|  
|트리거|**SSMA는 다음 트리거 의미 체계를 매핑합니다.**<br /><br />모든 행 트리거 후 /<br /><br />각 문은 /FOR 후 트리거<br /><br />하기 전에 모든 행에 대 한 및 INSTEAD OF / / 모든 행 트리거|  
|시퀀스|매핑됩니다.|  
|SELECT 문|**SSMA maps는 다음과 같은 예외를 사용 하 여 선택합니다.**<br /><br />변경 테이블 참조 데이터 절-부분적으로 매핑된 하지만 최종 테이블은 지원 되지 않습니다.<br /><br />테이블 참조 절-부분적으로 매핑된 analyze_table 등과 식만-테이블-참조, 외부 테이블 참조 되지만 컬렉션 파생 테이블, xmltable 식 SQL server 의미 체계에 매핑되지 않은<br /><br />기간 사양 절-매핑되지 않습니다.<br /><br />계속 처리기 절-매핑되지 않습니다.<br /><br />형식화 된 상관 관계 절-매핑되지 않습니다.<br /><br />동시 액세스 해상도 절-매핑되지 않습니다.|  
|VALUES 문|매핑됩니다.|  
|INSERT 문|매핑됩니다.|  
|UPDATE 문|S**SMA는 다음과 같은 예외를 사용 하 여 업데이트를 매핑합니다.**<br /><br />SQL server 의미 체계 절의 테이블 참조만-테이블-참조 매핑되지 않음<br /><br />기간 절-매핑되어 있지 않습니다.|  
|MERGE 문|**SSMA는 다음과 같은 예외를 사용 하 여 병합을 매핑합니다.**<br /><br />각 절에 여러 번 vs single-각 절의 제한 된 항목에 대 한 SQL server 의미 체계에 매핑된<br /><br />신호 절-SQL Server 의미 체계에 매핑되지 않는 경우<br /><br />혼합 된 업데이트 및 삭제 절-SQL Server 의미 체계에 매핑되지 않는<br /><br />기간-절-SQL Server 의미 체계에 매핑되지 않는 경우|  
|DELETE 문|**SSMA maps는 다음과 같은 예외를 사용 하 여 삭제합니다.**<br /><br />SQL server 의미 체계 절의 테이블 참조만-테이블-참조 매핑되지 않음<br /><br />기간 절-SQL Server 의미 체계에 매핑되지 않는 경우|  
|격리 수준 및 잠금 유형|매핑됩니다.|  
|프로시저 (SQL)|매핑됩니다.|  
|프로시저 (외부)|수동 업데이트를 해야 합니다.|  
|프로시저 (원본)|SQL Server 의미 체계에 매핑되지 않습니다.|  
|대입문|매핑됩니다.|  
|문을 프로시저 호출|매핑됩니다.|  
|CASE 문|매핑됩니다.|  
|FOR 문|매핑됩니다.|  
|GOTO 문|매핑됩니다.|  
|IF 문|매핑됩니다.|  
|반복 문|매핑됩니다.|  
|문을 그대로 둡니다.|매핑됩니다.|  
|반복 문|매핑됩니다.|  
|반복 문|매핑됩니다.|  
|문을 RESIGNAL합니다|조건이 지원 되지 않습니다. 메시지는 선택 사항이 될 수 있습니다.|  
|RETURN 문|매핑됩니다.|  
|신호 문|조건이 지원 되지 않습니다. 메시지는 선택 사항이 될 수 있습니다.|  
|WHILE 문|매핑됩니다.|  
|GET 진단 문|**SSMA는 다음과 같은 예외를 사용 하 여 진단 가져오기를 매핑합니다.**<br /><br />ROW_COUNT-매핑됩니다.<br /><br />DB2_RETURN_STATUS-매핑됩니다.<br /><br />MESSAGE_TEXT-매핑됩니다.<br /><br />DB2_SQL_NESTING_LEVEL-SQL Server 의미 체계에 매핑되지 않는 경우<br /><br />DB2_TOKEN_STRING-SQL Server 의미 체계에 매핑되지 않는 경우|  
|커서|**SSMA는 다음과 같은 예외를 사용 하 여 커서를 매핑합니다.**<br /><br />할당 커서 문-SQL Server 의미 체계에 매핑되지 않는 경우<br /><br />연결 로케이터 문-SQL Server 의미 체계에 매핑되지 않는 경우<br /><br />DECLARE CURSOR 문에-Returnability 절 SQL server 의미 체계에 매핑되어 있지 않습니다.<br /><br />FETCH 문이-부분 매핑을 합니다. 대상으로 하는 변수는만 지원 됩니다. SQL server 의미 체계 SQLDA 설명자 매핑되지 않음|  
|변수|매핑됩니다.|  
|예외, 처리기 및 조건|**SSMA는 다음과 같은 예외를 사용 하 여 "예외 처리를"를 매핑합니다.**<br /><br />종료 처리기-매핑됩니다.<br /><br />처리기 실행 취소-매핑됩니다.<br /><br />계속 처리기는 매핑되지 않습니다.<br /><br />조건-것에 매핑되지 않는 경우 SQL server 의미 체계.|  
|동적 SQL|매핑되지 않습니다.|  
|별칭|매핑됩니다.|  
|애칭|부분 매핑입니다. 기본 개체에 대 한 필요한 수동 처리|  
|동의어|매핑됩니다.|  
|DB2의 표준 함수|SSMA는 SQL Server에서 사용 가능한 경우 DB2 표준 함수를 매핑합니다.|  
|Authorization|매핑되지 않습니다.|  
|조건자|매핑됩니다.|  
|SELECT INTO 문|매핑되지 않습니다.|  
|값 INTO 문|매핑되지 않습니다.|  
|트랜잭션 제어|매핑되지 않습니다.|  
  
## <a name="converting-db2-database-objects"></a>DB2 데이터베이스 개체 변환  
DB2 데이터베이스 개체를 변환 하려면 먼저 변환 하려는 개체를 선택 및 SSMA 변환을 수행 해야 합니다. 변환 하는 동안 출력 메시지를 볼 수는 **뷰** 메뉴에서 **출력**합니다.  
  
**SQL Server 구문 DB2 개체 변환**  
  
1.  DB2 메타 데이터 탐색기에서 DB2 서버를 확장 한 다음 확장 **스키마**합니다.  
  
2.  변환할 개체를 선택 합니다.  
  
    -   모든 스키마로 변환 하려면 확인란을 선택 합니다 옆 **스키마**합니다.  
  
    -   를 변환 하거나 데이터베이스를 생략 하려면 스키마 이름 옆의 확인란을 선택 합니다.  
  
    -   를 변환 하거나 개체의 범주를 생략 하려면 스키마를 확장 한 다음 선택 하거나 범주 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개별 개체를 생략 하려면 범주 폴더를 확장 한 다음 선택 하거나 개체 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 마우스 오른쪽 단추로 클릭 **스키마** 선택한 **스키마 변환**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체 또는 개체 범주의 변환할 수도 있습니다 **스키마 변환**합니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 DB2 개체를 변환 될 수 있습니다. 변환 요약 보고서를 확인 하 여 성공 전환율을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  DB2 메타 데이터 탐색기에서 선택 **스키마**합니다.  
  
2.  오른쪽 창에서 선택 합니다 **보고서** 탭 합니다.  
  
    이 보고서는 평가 되거나 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 DB2 메타 데이터 탐색기에서 스키마를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 DB2 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 발생 하는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환에 실패 한 개체에 대 한 변환 오류가 발생 하는 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  DB2 메타 데이터 탐색기에서 확장 **스키마**합니다.  
  
2.  빨간색 오류 아이콘을 보여 주는 스키마를 확장 합니다.  
  
3.  스키마에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
5.  오른쪽 창에서을 클릭 합니다 **보고서** 탭 합니다.  
  
6.  맨 위에 있는 합니다 **보고서** 탭은 드롭 다운 목록. 목록에 표시 되 면 **통계**, 선택 영역을 변경 **원본**합니다.  
  
    SSMA는 소스 코드 및 코드 바로 위의 여러 개의 단추가 표시 됩니다.  
  
7.  클릭 합니다 **문제** 단추입니다. 이것이 오른쪽을 가리키는 화살표를 사용 하 여 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 찾은 첫 번째 문제가 있는 소스 코드를 강조 표시 됩니다.  
  
변환 될 수 있는 각 항목에 대해 해당 개체를 사용 하 여 수행 하려는 항목을 확인 해야 합니다.  
  
-   프로시저에 대 한 소스 코드를 수정할 수 있습니다 합니다 **SQL** 탭 합니다.  
  
-   DB2 데이터베이스를 제거 하거나 수정 하는 문제가 있는 코드에서 개체를 수정할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하는 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [DB2 데이터베이스에 연결 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)합니다.  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기 및 DB2 메타 데이터 탐색기, 개체를 로드 하기 전에 항목 옆의 확인란의 선택을 취소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 DB2에서 데이터를 마이그레이션.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스에서 다음 단계 [SQL Server로 변환된 된 개체를 로드](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)합니다.  
  
## <a name="see-also"></a>관련 항목  
[DB2 데이터를 SQL Server로 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
