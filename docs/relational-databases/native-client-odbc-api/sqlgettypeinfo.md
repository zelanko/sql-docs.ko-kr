---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a0f52c2a1bb2826126ae6548cfad95c5ccf5eac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85788064"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 **SQLGetTypeInfo**의 결과 집합에 추가 열 USERTYPE를 보고 합니다. USERTYPE은 DB-Library 데이터 형식 정의를 보고하며 기존 DB-Library 애플리케이션을 ODBC에 이식할 때 개발자가 이 기능을 이용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 ID를 특성으로 처리하지만 ODBC에서는 데이터 형식으로 처리합니다. 이러한 불일치를 해결 하기 위해 **SQLGetTypeInfo** 는 **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**및 **numericidentity**데이터 형식을 반환 합니다. **SQLGetTypeInfo** result set 열 AUTO_UNIQUE_VALUE는 이러한 데이터 형식에 대해 TRUE 값을 보고 합니다.  
  
 **Varchar**, **nvarchar** 및 **VARBINARY**의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 실제로 제한이 없더라도 COLUMN_SIZE 값에 대해 각각 8000, 4000 및 8000을 보고 합니다. 이는 이전 버전과의 호환성을 위한 것입니다.  
  
 **Xml** 데이터 형식의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 크기를 제한 하지 COLUMN_SIZE SQL_SS_LENGTH_UNLIMITED 보고 합니다.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 및 테이블 반환 매개 변수  
 테이블 반환 매개 변수의 테이블 형식은 실질적으로 메타 형식 즉, 다른 형식을 정의 하는 데 사용 되는 형식입니다. 따라서 SQLGetTypeInfo를 통해 노출 될 필요가 없습니다. 응용 프로그램은 SQLGetTypeInfo이 아닌 SQLTables를 사용 하 여 테이블 반환 매개 변수와 함께 사용 되는 테이블 형식에 대 한 메타 데이터를 검색 해야 합니다.  
  
 테이블 반환 매개 변수에 대 한 metdata를 검색 하는 방법에 대 한 자세한 내용은 [테이블 반환 매개 변수에 영향을 주는 문 특성](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)을 참조 하세요.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetTypeInfo 지원  
 날짜/시간 형식에 대해 반환 되는 값은 [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)를 참조 하세요.  
  
 보다 일반적인 정보는 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetTypeInfo 지원  
 **SQLGetTypeInfo** 는 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetTypeInfo 함수](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
