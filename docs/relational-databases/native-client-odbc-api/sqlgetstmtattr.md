---
title: SQLGetStmtAttr | Microsoft Docs
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
ms.openlocfilehash: be21c239bd01dea39022a75a3220f7093b4a3bef
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000358"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 SQLGetStmtAttr를 확장 하 여 드라이버별 문 특성을 노출 합니다.  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 에서는 읽기 및 쓰기 문 특성을 나열합니다. 이 항목에서는 읽기 전용 문 특성을 나열합니다.  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 특성은 명령 일괄 처리의 현재 명령을 노출합니다. 반환 값은 일괄 처리에서 명령의 위치를 지정하는 정수 값입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 특성은 NOCOUNT 옵션의 현재 설정을 나타냅니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLRowCount [를 호출할 때](../../relational-databases/native-client-odbc-api/sqlrowcount.md) 가 문의 영향을 받는 행 수를 보고할지 여부를 제어합니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT가 OFF입니다. SQLRowCount는 영향을 받는 행의 수를 반환 합니다.|  
|SQL_NC_ON|NOCOUNT가 ON입니다. 영향을 받는 행 수는 SQLRowCount에서 반환 되지 않으며 반환 된 값은 0입니다.|  
  
 SQLRowCount가 0을 반환 하는 경우 응용 프로그램은 SQL_SOPT_SS_NOCOUNT_STATUS를 테스트 해야 합니다. SQL_NC_ON 반환 되는 경우 SQLRowCount의 값 0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 행 개수를 반환 하지 못했음을 나타냅니다. SQL_NC_OFF가 반환되는 경우 NOCOUNT가 해제되어 있음을 의미하고, SQLRowCount 값 0은 문이 어떤 행에도 적용되지 않았음을 나타냅니다.  
  
 SQL_SOPT_SS_NOCOUNT_STATUS가 SQL_NC_OFF인 경우에는 응용 프로그램에서 SQLRowCount 값을 표시하면 안 됩니다. 대규모 일괄 처리나 저장 프로시저에서는 여러 개의 SET NOCOUNT 문을 포함할 수 있으므로 SQL_SOPT_SS_NOCOUNT_STATUS가 일정하게 유지되지 않을 수 있습니다. SQLRowCount가 0을 반환할 때마다이 옵션을 테스트 해야 합니다.  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 특성은 쿼리 알림 요청에 대한 메시지 텍스트를 반환합니다.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 및 테이블 반환 매개 변수  
 SQLGetStmtAttr를 호출 하 여 테이블 반환 매개 변수를 사용할 때 APD (응용 프로그램 매개 변수 설명자)의 SQL_SOPT_SS_PARAM_FOCUS 값을 가져올 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLSetStmtAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
