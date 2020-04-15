---
title: SQLGetStmtAttr | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f59b7f006387beea3d213b7f120e567487232e69
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282089"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 SQLGetStmtAttr을 확장하여 드라이버별 문 특성을 노출합니다.  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 에서는 읽기 및 쓰기 문 특성을 나열합니다. 이 항목에서는 읽기 전용 문 특성을 나열합니다.  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 특성은 명령 일괄 처리의 현재 명령을 노출합니다. 반환 값은 일괄 처리에서 명령의 위치를 지정하는 정수 값입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 특성은 NOCOUNT 옵션의 현재 설정을 나타냅니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLRowCount [를 호출할 때](../../relational-databases/native-client-odbc-api/sqlrowcount.md) 가 문의 영향을 받는 행 수를 보고할지 여부를 제어합니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT가 OFF입니다. SQLRowCount는 영향을 받는 행 수를 반환합니다.|  
|SQL_NC_ON|NOCOUNT가 ON입니다. 영향을 받는 행 수는 SQLRowCount에서 반환되지 않으며 반환된 값은 0입니다.|  
  
 SQLRowCount가 0을 반환하면 응용 프로그램은 SQL_SOPT_SS_NOCOUNT_STATUS 테스트해야 합니다. SQL_NC_ON 반환되는 경우 SQLRowCount의 0 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 행 수를 반환하지 않은 값만 나타냅니다. SQL_NC_OFF가 반환되는 경우 NOCOUNT가 해제되어 있음을 의미하고, SQLRowCount 값 0은 문이 어떤 행에도 적용되지 않았음을 나타냅니다.  
  
 SQL_SOPT_SS_NOCOUNT_STATUS가 SQL_NC_OFF인 경우에는 응용 프로그램에서 SQLRowCount 값을 표시하면 안 됩니다. 대규모 일괄 처리나 저장 프로시저에서는 여러 개의 SET NOCOUNT 문을 포함할 수 있으므로 SQL_SOPT_SS_NOCOUNT_STATUS가 일정하게 유지되지 않을 수 있습니다. 이 옵션은 SQLRowCount가 0을 반환할 때마다 테스트해야 합니다.  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 특성은 쿼리 알림 요청에 대한 메시지 텍스트를 반환합니다.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 및 테이블 반환 매개 변수  
 SQLGetStmtAttr 테이블 값 매개 변수로 작업할 때 응용 프로그램 매개 변수 설명자(APD)에서 SQL_SOPT_SS_PARAM_FOCUS 값을 얻기 위해 호출할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLSetStmtAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
