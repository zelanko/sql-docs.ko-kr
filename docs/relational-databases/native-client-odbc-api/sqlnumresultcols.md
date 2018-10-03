---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b240a9f9e2aa31ac40d134220d12711775008e0d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683371"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  실행된 된 문의 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합에서 열 수를 보고 서버를 방문 하지 않습니다. 이 경우 **SQLNumResultCols** 를 호출하더라도 서버 왕복은 발생하지 않습니다. 와 같은 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 하 고 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)를 호출 **SQLNumResultCols** 준비 되었지만 실행된 되지 않은 문에 서버 왕복이 생성 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 결과 집합 열의 수가 하나에서 다른 수로 변경될 수 있습니다. 이 경우 각 집합에 대해**SQLNumResultCols** 를 호출해야 합니다. 열 수가 변경되면 응용 프로그램이 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 집합 반환을 여러 결과 처리 하는 방법에 대 한 자세한 내용은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)합니다.  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLNumResultCols 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 SQLNumResultCols 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SQLNumResultCols 함수](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
