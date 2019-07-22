---
title: Transact-SQL 편집기 옵션 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_GRID
- sql.data.tools.SqlExecutionAdvancedSettingsOption
- sql.data.tools.SqlExecutionAnsiSettingsDlg
- sql.data.tools.SqlResultToTextSettingsDlg
- sql.data.tools.SqlExecutionGeneralSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.GENERAL
- sql.data.tools.unittesting.tsqleditor
- sql.data.tools.SqlResultsToGridSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.EDITOR_TAB_AND_STATUS_BAR
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_TEXT
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ANSI
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.ONLINE_EDITING
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ADVANCED
ms.assetid: fa9a250f-7feb-433e-91bd-a09779d74c8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5de3a6bef68955611290cce77b95989b7ff72c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110629"
---
# <a name="transact-sql-editor-options"></a>Transact-SQL 편집기 옵션
이 항목에서는 Transact-SQL 편집기의 일부 옵션에 대한 정보를 제공합니다. 이러한 옵션을 설정하려면 **옵션** 대화 상자에서 **도구\옵션** 메뉴로 이동합니다.  
  
[쿼리 실행](#QueryExecution)  
  
[쿼리 결과](#QueryResults)  
  
## <a name="QueryExecution"></a>쿼리 실행  
  
|속성|설명|  
|------------|---------------|  
|**SET ROWCOUNT**|기본값 0은 모든 결과를 받을 때까지 SQL Server에서 결과를 기다린다는 것을 나타냅니다. SQL Server에서 지정한 행 수를 받은 후 쿼리를 중단하려면 0보다 큰 값을 지정합니다. 모든 행이 반환될 수 있도록 이 옵션을 해제하려면 SET ROWCOUNT 0을 지정합니다.|  
|**SET TEXTSIZE**|기본값 2,147,483,647바이트는 SQL Server에서 text, ntext, nvarchar(max) 및 varchar(max) 데이터 필드의 제한까지 전체 데이터 필드를 제공한다는 것을 나타냅니다. XML 데이터 형식에는 영향을 주지 않습니다. 값이 클 경우 결과를 제한하려면 보다 작은 수를 지정합니다. 지정한 수보다 많은 열은 잘립니다.|  
|**실행 제한 시간**|쿼리를 취소할 때까지 기다리는 시간(초)을 나타냅니다. 값 0은 무한 대기 또는 제한 시간 없음을 의미합니다.|  
|**기본적으로 SQLCMD 모드로 새 쿼리를 엽니다.**|SQLCMD 모드로 새 쿼리를 열려면 이 확인란을 선택합니다. 이 확인란은 도구 메뉴를 통해 대화 상자를 연 경우에만 표시됩니다.<br /><br />이 옵션을 선택할 경우 다음과 같은 제한 사항에 유의해야 합니다.<br /><br />-   데이터베이스 엔진 쿼리 편집기에서 IntelliSense는 해제되어 있습니다.<br />-   쿼리 편집기를 명령줄에서 실행하지 못하므로 변수와 같은 명령줄 매개 변수를 전달할 수 없습니다.<br />-   쿼리 편집기는 운영 체제 프롬프트에 응답할 수 없으므로 대화형 문을 실행하지 않도록 주의해야 합니다.|  
|**SET NOCOUNT**|Transact-SQL 문의 영향을 받은 행 수를 나타내는 메시지가 결과의 일부로 반환되지 않도록 합니다. 자세한 내용은 [SET NOCOUNT](https://go.microsoft.com/fwlink/?LinkID=238731)를 참조하십시오.|  
|**SET NOEXEC**|**ON**으로 설정하면 Microsoft® SQL Server™가 Transact-SQL 문의 각 일괄 처리를 컴파일하지만 실행하지는 않습니다. **OFF**로 설정하면 Microsoft® SQL Server™가 컴파일 후 모든 일괄 처리를 실행합니다. 자세한 내용은 [SET NOEXEC](https://go.microsoft.com/fwlink/?LinkId=238770)를 참조하세요.|  
|**SET PARSEONLY**|각 Transact-SQL 문의 구문을 검사한 후 문을 컴파일하거나 실행하지 않고 오류 메시지를 반환합니다. 자세한 내용은 [SET PARSEONLY](https://go.microsoft.com/fwlink/?LinkId=238734)를 참조하십시오.|  
|**SET CONCAT_NULL_YIELDS_NULL**|연결 결과를 Null 값으로 처리할지 빈 문자열 값으로 처리할지 여부를 제어합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL](https://go.microsoft.com/fwlink/?LinkId=238733)을 참조하세요.|  
|**SET ARITHABORT**|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다. 자세한 내용은 [SET ARITHABORT](https://msdn.microsoft.com/library/aa259212(v=SQL.80).aspx)를 참조하세요.|  
|**SET SHOWPLAN_TEXT**|Microsoft® SQL Server™가 Transact-SQL 문을 실행하지 않도록 합니다. 대신 SQL Server는 문 실행 방법에 대한 자세한 정보를 반환합니다. 자세한 내용은 [SET SHOWPLAN_TEXT](https://go.microsoft.com/fwlink/?LinkID=238737)를 참조하세요.|  
|**SET STATISTICS TIME**|각 문을 구문 분석, 컴파일 및 실행하는 데 필요한 시간(밀리초)을 표시합니다.|  
|**SET STATISTICS IO**|Microsoft® SQL Server™가 Transact-SQL 문에 의해 생성된 디스크 작동 크기에 대한 정보를 표시하도록 합니다.|  
|**SET TRANSACTION ISOLATION LEVEL**|연결하여 실행되는 모든 Microsoft® SQL Server™ **SELECT** 문의 기본 트랜잭션 잠금 동작을 제어합니다. 자세한 내용은  [SET TRANSACTION ISOLATION LEVEL](https://go.microsoft.com/fwlink/?LinkId=238730)을 참조하십시오.|  
|**SET LOCK_TIMEOUT**|잠금이 해제될 때가지 문이 기다려야 할 시간(밀리초)을 지정합니다. 자세한 내용은 [SET LOCK_TIMEOUT](https://go.microsoft.com/fwlink/?LinkId=238747)을 참조하세요.|  
|**SET QUERY_GOVERNOR_COST_LIMIT**|현재 연결에 대해 구성되어 있는 값을 재정의합니다. 자세한 내용은 [SET QUERY_GOVERNOR_COST_LIMIT](https://go.microsoft.com/fwlink/?LinkId=238749)을 참조하세요.|  
|**SET ANSI_DEFAULTS**|SQL-92 표준 동작 일부를 전체적으로 지정하는 Microsoft® SQL Server™ 설정 그룹을 제어합니다. 자세한 내용은 [SET ANSI_DEFAULTS](https://go.microsoft.com/fwlink/?LinkId=238750)를 참조하세요.|  
|**SET QUOTED_IDENTIFIER**|Microsoft® SQL Server™가 인용 부호 구분 식별자 및 리터럴 문자열에 관해 SQL-92 규칙을 따르도록 합니다. 큰따옴표로 구분된 식별자는 Transact-SQL의 예약된 키워드이거나 Transact-SQL 식별자 구문 규칙에서 허용하지 않는 문자를 포함할 수 있습니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](https://go.microsoft.com/fwlink/?LinkId=238751)를 참조하세요.|  
|**SET ANSI_NULL_DFLT_ON**|데이터베이스의 ANSI Null 기본값 옵션이 false로 설정되어 있으면 세션의 동작을 변경하여 새 열의 기본 Null 허용 여부보다 우선 적용됩니다. 자세한 내용은 [SET ANSI_NULL_DFLT_ON](https://go.microsoft.com/fwlink/?LinkID=238752)을 참조하세요.|  
|**SET IMPLICIT_TRANSACTIONS**|**ON**으로 설정하면 연결이 암시적 트랜잭션 모드로 설정됩니다. **OFF**로 설정하면 연결이 다시 자동 커밋 트랜잭션 모드로 돌아갑니다. 자세한 내용은 [SET IMPLICIT_TRANSACTIONS](https://go.microsoft.com/fwlink/?LinkId=238753)를 참조하세요.|  
|**SET CURSOR_CLOSE_ON_COMMIT**|트랜잭션을 커밋할 때 커서를 닫을 것인지를 제어합니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT](https://go.microsoft.com/fwlink/?LinkId=238754)을 참조하세요.|  
|**SET ANSI_PADDING**|열이 정의된 열 크기보다 짧은 값을 저장하는 방법과 **char**, **varchar**, **binary**및 **varbinary** 데이터에 후행 공백이 있는 값을 저장하는 방법을 제어합니다. 자세한 내용은 [SET ANSI_PADDING](https://go.microsoft.com/fwlink/?LinkId=238755)을 참조하세요.|  
|**SET ANSI_WARNINGS**|여러 오류 조건에 대한 SQL-92 표준 동작을 지정합니다. 자세한 내용은 [SET ANSI_WARNINGS](https://go.microsoft.com/fwlink/?LinkId=238758)를 참조하세요.|  
|**SET ANSI_NULLS**|Null 값과 함께 사용될 경우 Equals(**=**)와 Not Equal To(**<>**) 비교 연산자의 SQL-92 호환 동작을 지정합니다. 자세한 내용은 [SET ANSI_NULLS](https://go.microsoft.com/fwlink/?LinkId=238759)를 참조하세요.|  
  
## <a name="QueryResults"></a>쿼리 결과  
  
|속성|설명|  
|------------|---------------|  
|**결과 집합에 쿼리 포함**|결과 집합의 일부로 쿼리 텍스트를 반환합니다.|  
|**결과를 복사하거나 저장할 때 열 머리글 포함**|결과를 클립보드에 복사하거나 파일에 저장할 때 열 머리글(제목)을 포함합니다. 저장하거나 복사한 결과 데이터에 열 머리글 없이 데이터만 포함하려면 이 확인란의 선택을 취소합니다.|  
|**실행 후 결과 삭제**|화면에 표시한 후 쿼리 결과를 삭제하여 메모리를 확보합니다.|  
|**별도의 탭에 결과 표시**|쿼리 문서 창의 아래쪽 대신 새로운 문서 창에 결과 집합을 표시합니다.|  
|**쿼리 실행 후 결과 탭으로 전환**|자동으로 화면 포커스를 결과 집합에 둡니다.|  
|**검색한 최대 문자 수**|비 XML 데이터:<br /><br />1에서 65535 사이의 숫자를 입력하여 각 셀에 표시될 최대 문자 수를 지정합니다. **참고:** 너무 많은 문자를 지정하면 결과 집합의 데이터가 잘려 보일 수 있습니다. 각 셀에 표시되는 최대 문자 수는 글꼴 크기에 따라 달라집니다. 이 입력란에 높은 값을 입력하면 큰 결과 집합이 반환될 경우 SQL Server Management Studio의 메모리 실행 속도가 느려지거나 시스템 성능이 저하될 수 있습니다.<br /><br />XML 데이터:<br /><br />1MB, 2MB 또는 5MB를 선택합니다. 모든 문자를 검색하려면 제한 없음을 선택합니다.|  
|**출력 형식**|기본적으로 결과에 공백을 채워 만든 열에 출력됩니다. 이외에 쉼표, 탭 또는 공백을 사용하여 열을 구분하는 옵션이 있습니다. **사용자 지정 구분 기호** 입력란에 다른 구분 기호 문자를 지정하려면 **사용자 지정 구분 기호** 확인란을 선택합니다.|  
|**사용자 지정 구분 기호**|열을 구분할 문자를 지정합니다. 이 옵션은 **출력 형식** 상자에서 **사용자 지정 구분 기호** 확인란을 선택한 경우에만 사용할 수 있습니다.|  
|**결과 집합에 열 머리글 포함**|각 열에 열 제목을 붙이지 않으려면 이 확인란의 선택을 취소합니다.|  
|**결과를 받는 대로 스크롤**|아래쪽의 가장 최근에 반환된 레코드에 포커스를 표시하려면 이 확인란을 선택합니다. 받은 첫 번째 행에 포커스를 표시하려면 이 확인란의 선택을 취소합니다.|  
|**숫자 값 오른쪽 맞춤**|숫자 값을 열 오른쪽에 맞추려면 이 확인란을 선택합니다. 이 옵션을 선택하면 고정 소수 자릿수를 가진 숫자를 쉽게 검토할 수 있습니다.|  
|**쿼리 실행 후 결과 삭제**|화면에 표시한 후 쿼리 결과를 삭제하여 메모리를 확보합니다.|  
|**별도의 탭에 결과 표시**|쿼리 문서 창의 아래쪽 대신 새로운 문서 창에 결과 집합을 표시하려면 이 확인란을 선택합니다.|  
|**쿼리 실행 후 결과 탭으로 전환**|자동으로 화면 포커스를 결과 집합에 두려면 클릭합니다.|  
|**각 열에 표시할 최대 문자 수**|기본값은 256자입니다. 이보다 큰 결과 집합을 잘리지 않게 표시하려면 값을 높입니다.|  
|**기본값으로 다시 설정**|이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.|  
  
