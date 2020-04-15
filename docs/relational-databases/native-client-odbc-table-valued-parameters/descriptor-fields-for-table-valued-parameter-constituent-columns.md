---
title: 테이블 값 매개 변수에 대한 설명자 필드
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08074ad57ca4f0e4f7c2c56d9eca595baf595b5f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297861"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>테이블 반환 매개 변수 구성 열의 설명자 필드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 섹션에서 설명하는 테이블 값 매개 변수 설명자 필드는 구현 매개 변수 설명자(IPD)에 대한 핸들이 있는 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 및 [SQLSetDescField를](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 사용하여 조작됩니다.  
  
## <a name="remarks"></a>설명  
 SQL_DESC_AUTO_UNIQUE_VALUE는 테이블 반환 매개 변수뿐 아니라 다른 기능에 대해서도 사용됩니다.  
  
|특성 이름|Type|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE는 해당 열이 ID 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 정보를 사용하여 성능을 최적화할 수 있지만 응용 프로그램은 ID 열에 대해 설정할 필요가 없습니다.|  
||||

 APD(애플리케이션 매개 변수 설명자) 및 IPD의 모든 매개 변수 유형에는 다음과 같은 특성이 추가됩니다.  
  
|특성 이름|Type|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE는 해당 열이 계산 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 정보를 사용하여 성능을 최적화할 수 있지만 응용 프로그램은 계산된 열에 대해 설정할 필요가 없습니다.<br /><br /> 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE는 테이블 반환 매개 변수 열이 고유 키에 참여함을 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|테이블 반환 매개 변수 열의 정렬 순서를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 가능한 값은 다음과 같습니다. <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> **SQL_SS_ASCENDING_ORDER** SQL_SS_DESCENDING_ORDER 이외의 값은 **SQLSTATE HY024** 및 메시지 '잘못된 특성 값'으로 오류를 **생성하고** 이 특성의 기본값인 **SQL_SS_ORDER_UNSPECIFIED**로 처리됩니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|테이블 반환 매개 변수의 전체 순서를 정의하는 열 집합의 테이블 반환 매개 변수 열에 지정된 서수를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 정렬 서수는 1부터 시작합니다. 기본값 0은 테이블 반환 매개 변수 열에 열 순서가 지정되지 않았음을 나타냅니다.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|테이블 반환 매개 변수의 모든 행에 해당 열의 기본값이 지정될지 여부를 나타냅니다. 테이블 반환 매개 변수의 경우 기본값을 행 단위로 선택할 수 없습니다. SQL_FALSE 값은 기본값이 아닌 값이 행에 지정됨을 나타냅니다. 이것이 기본값입니다. SQL_TRUE 값은 모든 행의 기본값이 해당 열에 지정됨을 나타냅니다.<br /><br /> SQL_TRUE로 설정된 경우 서버로 데이터가 전송되지 않습니다.<br /><br /> 서버 처리에 열 값이 필요하지 않는 경우 이 필드를 ID 열이나 계산 열에서도 사용할 수 있습니다.|  
||||

 이러한 특성은 테이블 반환 매개 변수 열에 대해서만 유효하고 다른 매개 변수에 대해서는 무시됩니다.  
  
 SQL_CA_SS_COL_HAS_DEFAULT_VALUE가 테이블 반환 매개 변수 열에 대해 설정된 경우 해당 열의 SQL_DESC_DATA_PTR은 null 포인터여야 합니다. 그렇지 않으면 SQLExecute 또는 SQLExecDirect가 SQL_ERROR 반환합니다. 진단 레코드는 SQLSTATE=07S01 및 \<"매개 변수 p> 기본 매개 변수의 \<잘못된 사용, \<열 c>"이라는 메시지와 \<함께 생성되며 p> 매개 변수 서수 및 c> 열 서수입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 값 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
