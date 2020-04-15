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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303364"
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  메타데이터 검색 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 개선을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 통해 Native Client 응용 프로그램은 쿼리 실행에서 반환되는 열 또는 매개 변수 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 동일하거나 호환되도록 할 수 있습니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 bcp 및 ODBC 함수와 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 쿼리 출력 작업에서 메타데이터를 검색하지 않도록 지연된 읽기(지연된 메타데이터 검색)을 지정할 수 있습니다. 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 네이티브 클라이언트를 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 여 응용 프로그램을 개발 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]하지만 보다 이전 서버 버전에 연결 하는 경우 메타 데이터 검색 기능 서버의 버전에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 bcp 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   [bcp_columns](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 또한 [bcp_setbulkmode](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)을 사용하여 메타데이터 형식을 지정할 때 성능이 향상됩니다.  
  
 [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 동작을 제어하는 새로운 *전자 옵션이* bcp_control: **BCPDELAYREADFMT**.  
  
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
  
  
