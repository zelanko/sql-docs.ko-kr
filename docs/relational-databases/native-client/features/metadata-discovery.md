---
title: 메타데이터 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d822362e9f9f7e70e4421056383aae8ddef03dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303364"
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  의 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 메타 데이터 검색 개선 기능 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 사용 하면 Native Client 응용 프로그램에서 쿼리 실행 시 반환 된 열 또는 매개 변수 메타 데이터가 쿼리를 실행 하기 전에 지정한 메타 데이터 형식과 동일 하거나 호환 되는지 확인할 수 있습니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 bcp 및 ODBC 함수와 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 쿼리 출력 작업에서 메타데이터를 검색하지 않도록 지연된 읽기(지연된 메타데이터 검색)을 지정할 수 있습니다. 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 에서 Native Client를 사용 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 여 응용 프로그램 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 을 개발 하지만 이전 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]버전의 서버에 연결 하는 경우 메타 데이터 검색 기능은 서버 버전에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 bcp 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   [bcp_columns](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 [Bcp_setbulkmode](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)를 사용 하 여 메타 데이터 형식을 지정 하는 경우 성능 향상도 표시 됩니다.  
  
 [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 에는 **Bcpdelayreadfmt**bcp_readfmt의 동작을 제어 하는 새로운 *eoption* 가 있습니다.  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 ODBC 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../../relational-databases/native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 OLE DB 멤버 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters::GetParameterInfo(자세한 내용은 [ICommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md) 참조)  
  
 또한 IBCPSession::BCPSetBulkMode를 사용하여 메타데이터 형식을 지정하는 경우 향상된 성능을 경험할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 다음과 같은 두 개의 저장 프로시저가 추가되어 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client에서 메타데이터 검색 기능이 향상되었습니다.  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
