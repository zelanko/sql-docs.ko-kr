---
title: SQL프로시저칼럼 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b942126a5ad73d5c41f28f60a63d22ef8584f24
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280105"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLProcedureColumns는** 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장된 프로시저의 반환 값 특성을 보고하는 한 행을 반환합니다.  
  
 **SQLProcedureColumns는** *카탈로그 이름,* *스키마 이름,* *ProcName*또는 *ColumnName* 매개 변수에 대한 값이 있는지 여부를 SQL_SUCCESS 반환합니다. **SQLFetch는** 이러한 매개 변수에 잘못된 값이 사용되는 SQL_NO_DATA 반환합니다.  
  
 **SQLProcedureColumns** 정적 서버 커서에서 실행할 수 있습니다. 업데이터(동적 또는 키 집합) 커서에서 **SQLProcedureColumns를** 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환됩니다.  
  
 다음 표에는 결과 집합에서 반환되는 열과 네이티브 클라이언트 ODBC 드라이버를 통해 **udt** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 **xml** 데이터 형식을 처리하도록 확장된 열이 나열됩니다.  
  
|열 이름|설명|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름을 반환합니다.|  
|SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름을 반환합니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 정규화된 어셈블리 이름을 반환합니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름을 반환합니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|XML 스키마 컬렉션 이름이 정의된 스키마의 이름을 반환합니다. 스키마 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|XML 스키마 컬렉션의 이름을 반환합니다. 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns와 테이블 반환 매개 변수  
 SQLProcedureColumns는 CLR 사용자 정의 형식과 유사한 방식으로 테이블 값 매개 변수를 처리합니다. 테이블 반환 매개 변수에 대해 반환되는 행의 열은 다음과 같은 값을 갖습니다.  
  
|열 이름|설명/값|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|테이블 반환 매개 변수에 대한 테이블 유형의 이름입니다.|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|테이블 반환 매개 변수의 열 수입니다.|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|REMARKS|NULL|  
|COLUMN_DEF|NULL 테이블 유형에 기본값이 없을 수도 있습니다.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|테이블 또는 CLR 사용자 정의 형식을 포함하는 카탈로그의 이름을 반환합니다.|  
|SS_TYPE_SCHEMA_NAME|테이블 또는 CLR 사용자 정의 형식을 포함하는 스키마의 이름을 반환합니다.|  
  
 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME 열은 각각 테이블 반환 매개 변수의 카탈로그와 스키마를 반환하기 위해 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 사용 가능합니다. 두 열은 테이블 반환 매개 변수뿐만 아니라 CLR 사용자 정의 형식 매개 변수에 대해서도 채워집니다. CLR 사용자 정의 형식 매개 변수의 기존 스키마 및 카탈로그 열은 이 추가 기능의 영향을 받지 않습니다. 또한 두 열은 이전 버전과의 호환성을 유지하기 위해 채워집니다.  
  
 ODBC 사양에 따라 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 추가된 모든 드라이버별 열 앞에, 그리고 ODBC 자체에서 지정한 모든 열 뒤에 표시됩니다.  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLProcedureColumns 지원  
 날짜/시간 형식에 대해 반환된 값은 [카탈로그 메타데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)를 참조하십시오.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLProcedureColumns 지원  
 **SQLProcedureColumns는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL프로시저열 함수](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
