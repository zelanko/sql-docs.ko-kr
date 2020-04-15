---
title: SQLGetTypeInfo | 마이크로 소프트 문서
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
ms.openlocfilehash: 81ba57c6e66f156f13055ff5ec941fa8f0c86381
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298451"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 **SQLGetTypeInfo**의 결과 집합에서 추가 열 USERTYPE을 보고합니다. USERTYPE은 DB-Library 데이터 형식 정의를 보고하며 기존 DB-Library 애플리케이션을 ODBC에 이식할 때 개발자가 이 기능을 이용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 ID를 특성으로 처리하지만 ODBC에서는 데이터 형식으로 처리합니다. 이 불일치를 해결 하기 위해 **SQLGetTypeInfo** 데이터 형식을 반환: **intidentity,** **smallintidentity,** **작은**id, **소수점 ID**및 **숫자 id**. **SQLGetTypeInfo** 결과 집합 열 AUTO_UNIQUE_VALUE 이러한 데이터 형식에 대 한 TRUE 값을 보고 합니다.  
  
 **varchar,** **nvarchar** 및 **varbinary의** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 실제로 무제한임에도 불구하고 COLUMN_SIZE 값에 대해 각각 8000, 4000 및 8000을 보고합니다. 이는 이전 버전과의 호환성을 위한 것입니다.  
  
 **xml** 데이터 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 무제한 크기를 나타내기 위해 COLUMN_SIZE SQL_SS_LENGTH_UNLIMITED 보고합니다.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 및 테이블 반환 매개 변수  
 테이블 값 매개 변수에 대 한 테이블 형식은 효과적으로 메타 형식 즉, 다른 형식을 정의 하는 데 사용 되는 형식입니다. 따라서 SQLGetTypeInfo를 통해 노출 될 필요가 없습니다. 응용 프로그램은 SQLGetTypeInfo 대신 SQLTable을 사용하여 테이블 값 매개 변수와 함께 사용되는 테이블 형식에 대한 메타데이터를 검색해야 합니다.  
  
 자세한 내용은 테이블 값 매개 변수에 대한 metdata 검색에 대한 자세한 내용은 [테이블 값 매개 변수에 영향을 주는 문 특성을](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)참조하십시오.  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetTypeInfo 지원  
 날짜/시간 형식에 대해 반환된 값은 [카탈로그 메타데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)를 참조하십시오.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetTypeInfo 지원  
 **SQLGetTypeInfo는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetTypeInfo 함수](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
