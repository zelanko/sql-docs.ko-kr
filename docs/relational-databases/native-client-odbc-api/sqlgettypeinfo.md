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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6d813848a45326ee9a74ea38616ceef9dd02cd5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524049"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 보고서 결과에 추가 열 USERTYPE 집합이 **SQLGetTypeInfo**합니다. USERTYPE은 DB-Library 데이터 형식 정의를 보고하며 기존 DB-Library 응용 프로그램을 ODBC에 이식할 때 개발자가 이 기능을 이용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 ID를 특성으로 처리하지만 ODBC에서는 데이터 형식으로 처리합니다. 이러한 불일치를 해결 하려면 **SQLGetTypeInfo** 데이터 형식을 반환 합니다. **intidentity**를 **smallintidentity**, **tinyintidentity**, **decimalidentity**, 및 **numericidentity**합니다. 합니다 **SQLGetTypeInfo** 결과 집합 열 AUTO_UNIQUE_VALUE는 이러한 데이터 형식에 대해 TRUE 값을 보고 합니다.  
  
 에 대 한 **varchar**를 **nvarchar** 하 고 **varbinary**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 column_size 8000, 4000 및 8000을 각각 보고서 계속 실제로 제한 되지 않더라도 값입니다. 이는 이전 버전과의 호환성을 위한 것입니다.  
  
 에 대 한 합니다 **xml** 데이터 형식으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 column_size 무제한 크기를 표시 하는 SQL_SS_LENGTH_UNLIMITED를 보고 합니다.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 및 테이블 반환 매개 변수  
 테이블 반환 매개 변수에 대 한 테이블 형식은를 메타-유형-형식임을 다른 형식을 정의 하는 데 효과적으로입니다. 따라서 SQLGetTypeInfo를 통해 노출 될 필요가 없습니다. 응용 프로그램 테이블 반환 매개 변수를 사용 하는 테이블 형식에 대 한 메타 데이터를 검색할 SQLGetTypeInfo, 대신 SQLTables를 사용 해야 합니다.  
  
 테이블 반환 매개 변수의 메타 데이터를 검색 하는 방법에 대 한 자세한 내용은 참조 [문 특성 Affect Table-Valued 매개 변수는](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetTypeInfo 지원  
 날짜/시간 형식에 대 한 반환 값을 참조 하세요 [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)입니다.  
  
 자세한 내용은 참조 하세요. [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetTypeInfo 지원  
 **SQLGetTypeInfo** 큰 CLR 사용자 정의 형식 (Udt)를 지원 합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLGetTypeInfo 함수](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
