---
title: 테이블 반환 매개 변수 구성 열의 설명자 필드 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b86145c43b072361b20d1e7e8869091689fb831
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>테이블 반환 매개 변수 구성 열의 설명자 필드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 섹션에서 설명 하는 테이블 반환 매개 변수 설명자 필드를 사용 하 여 조작 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 및 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 구현 매개 변수 설명자 (에 대 한 핸들을 포함 IPD)입니다.  
  
## <a name="remarks"></a>주의  
 SQL_DESC_AUTO_UNIQUE_VALUE는 테이블 반환 매개 변수뿐 아니라 다른 기능에 대해서도 사용됩니다.  
  
|특성 이름|형식|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE는 해당 열이 ID 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능을 최적화 하기 위해이 정보를 사용할 수 있지만 응용 프로그램 id 열에 설정 하지 않아도 됩니다.|  
  
 APD(응용 프로그램 매개 변수 설명자) 및 IPD의 모든 매개 변수 유형에는 다음과 같은 특성이 추가됩니다.  
  
|특성 이름|형식|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE는 해당 열이 계산 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능을 최적화 하기 위해이 정보를 사용할 수 있지만 계산된 열에 대 한 설정 하려면 응용 프로그램은 필요 하지 않습니다.<br /><br /> 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE는 테이블 반환 매개 변수 열이 고유 키에 참여함을 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|테이블 반환 매개 변수 열의 정렬 순서를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 가능한 값은 다음과 같습니다. <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> 이외의 값 **SQL_SS_ASCENDING_ORDER** 및 **SQL_SS_DESCENDING_ORDER** 오류가 생성 **SQLSTATE HY024** 하 고 '잘못 된 특성 값' 메시지와 로 처리 **SQL_SS_ORDER_UNSPECIFIED**,이 특성에 대 한 기본값은입니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|테이블 반환 매개 변수의 전체 순서를 정의하는 열 집합의 테이블 반환 매개 변수 열에 지정된 서수를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 정렬 서수는 1부터 시작합니다. 기본값 0은 테이블 반환 매개 변수 열에 열 순서가 지정되지 않았음을 나타냅니다.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|테이블 반환 매개 변수의 모든 행에 해당 열의 기본값이 지정될지 여부를 나타냅니다. 테이블 반환 매개 변수의 경우 기본값을 행 단위로 선택할 수 없습니다. SQL_FALSE 값은 기본값이 아닌 값이 행에 지정됨을 나타냅니다. 기본값입니다. SQL_TRUE 값은 모든 행의 기본값이 해당 열에 지정됨을 나타냅니다.<br /><br /> SQL_TRUE로 설정된 경우 서버로 데이터가 전송되지 않습니다.<br /><br /> 서버 처리에 열 값이 필요하지 않는 경우 이 필드를 ID 열이나 계산 열에서도 사용할 수 있습니다.|  
  
 이러한 특성은 테이블 반환 매개 변수 열에 대해서만 유효하고 다른 매개 변수에 대해서는 무시됩니다.  
  
 SQL_CA_SS_COL_HAS_DEFAULT_VALUE가 테이블 반환 매개 변수 열에 대해 설정된 경우 해당 열의 SQL_DESC_DATA_PTR은 null 포인터여야 합니다. 그렇지 않으면, SQLExecute 또는 SQLExecDirect SQL_ERROR를 반환 합니다. Sqlstate 진단 레코드가 생성 됩니다 = 07S01 및 "매개 변수에 대 한 기본 매개 변수를 잘못 사용 \<p >, 열 \<c >", 여기서 \<p >는 매개 변수 서 수 및 \<c >은 열 서 수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
