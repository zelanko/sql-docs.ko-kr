---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c22467069614bdfdd3979b7d74bb9261297225a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32943828"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 보고서의 결과에서 추가 열 USERTYPE 집합 **SQLGetTypeInfo**합니다. USERTYPE은 DB-Library 데이터 형식 정의를 보고하며 기존 DB-Library 응용 프로그램을 ODBC에 이식할 때 개발자가 이 기능을 이용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 ID를 특성으로 처리하지만 ODBC에서는 데이터 형식으로 처리합니다. 이러한 불일치를 해결 하려면 **SQLGetTypeInfo** 반환 데이터 형식: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**, 및 **numericidentity**합니다. **SQLGetTypeInfo** 결과 집합 열 AUTO_UNIQUE_VALUE는 이러한 데이터 형식에 대해 TRUE 값을 보고 합니다.  
  
 에 대 한 **varchar**, **nvarchar** 및 **varbinary**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 COLUMN_SIZE에 대해 8000, 4000 및 8000을 각각 보고할 계속 값을 하지만 실제로 제한 되지 않습니다. 이는 이전 버전과의 호환성을 위한 것입니다.  
  
 에 대 한는 **xml** 데이터 형식으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 크기 제한이 나타내기 위해 COLUMN_SIZE SQL_SS_LENGTH_UNLIMITED를 보고 합니다.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 및 테이블 반환 매개 변수  
 테이블 반환 매개 변수의 테이블 형식은 실제적으로 메타 형식 즉, 다른 형식을 정의하는 데 사용되는 형식입니다. 따라서 것은 아닙니다 SQLGetTypeInfo 통해 노출 될 수 있습니다. 응용 프로그램에는 테이블 반환 매개 변수와 함께 사용 되는 테이블 형식에 대 한 메타 데이터를 검색 SQLGetTypeInfo, 보다는 SQLTables를 사용 해야 합니다.  
  
 테이블 반환 매개 변수의 메타 데이터를 검색 하는 방법에 대 한 자세한 내용은 참조 [문 Affect Table-Valued 매개 변수 특성](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 사용 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetTypeInfo 지원  
 날짜/시간 형식에 대해 반환 되는 값을 참조 하십시오. [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)합니다.  
  
 자세한 내용은 참조 하십시오. [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetTypeInfo 지원  
 **SQLGetTypeInfo** 큰 CLR 사용자 정의 형식 (Udt)을 지원 합니다. 자세한 내용은 참조 [Large CLR User-Defined 형식 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLGetTypeInfo 함수](http://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
