---
title: 테이블 반환 매개 변수의 설명자 필드
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
ms.openlocfilehash: 4fc2ea564bff8899b3df82fd5d82297b7997c08c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783209"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>테이블 반환 매개 변수 구성 열의 설명자 필드
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  이 섹션에서 설명 하는 테이블 반환 매개 변수 설명자 필드는 IPD (구현 매개 변수 설명자)의 핸들과 함께 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 및 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) 를 사용 하 여 조작 합니다.  
  
## <a name="remarks"></a>설명  
 SQL_DESC_AUTO_UNIQUE_VALUE는 테이블 반환 매개 변수뿐 아니라 다른 기능에 대해서도 사용됩니다.  
  
|특성 이름|형식|설명|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE는 해당 열이 ID 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는이 정보를 사용 하 여 성능을 최적화할 수 있지만 응용 프로그램은 id 열에 대해이 정보를 설정할 필요가 없습니다.|  
||||

 APD(애플리케이션 매개 변수 설명자) 및 IPD의 모든 매개 변수 유형에는 다음과 같은 특성이 추가됩니다.  
  
|특성 이름|형식|설명|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE는 해당 열이 계산 열임을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는이 정보를 사용 하 여 성능을 최적화할 수 있지만 응용 프로그램에서 계산 열에 대해이 정보를 설정할 필요는 없습니다.<br /><br /> 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE는 테이블 반환 매개 변수 열이 고유 키에 참여함을 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|테이블 반환 매개 변수 열의 정렬 순서를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 가능한 값은 다음과 같습니다. <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> **SQL_SS_ASCENDING_ORDER** 및 **SQL_SS_DESCENDING_ORDER** 이외의 값은 **SQLSTATE HY024** 및 message ' 잘못 된 특성 값 '이 포함 된 오류를 생성 하 고이 특성의 기본값인 **SQL_SS_ORDER_UNSPECIFIED**으로 처리 됩니다.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|테이블 반환 매개 변수의 전체 순서를 정의하는 열 집합의 테이블 반환 매개 변수 열에 지정된 서수를 나타냅니다. 이 경우 쿼리 성능이 향상될 수 있습니다. 테이블 반환 매개 변수 열이 아닌 바인딩에 대해서는 이 특성이 무시됩니다. 정렬 서수는 1부터 시작합니다. 기본값 0은 테이블 반환 매개 변수 열에 열 순서가 지정되지 않았음을 나타냅니다.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|테이블 반환 매개 변수의 모든 행에 해당 열의 기본값이 지정될지 여부를 나타냅니다. 테이블 반환 매개 변수의 경우 기본값을 행 단위로 선택할 수 없습니다. SQL_FALSE 값은 기본값이 아닌 값이 행에 지정됨을 나타냅니다. 기본값입니다. SQL_TRUE 값은 모든 행의 기본값이 해당 열에 지정됨을 나타냅니다.<br /><br /> SQL_TRUE로 설정된 경우 서버로 데이터가 전송되지 않습니다.<br /><br /> 서버 처리에 열 값이 필요하지 않는 경우 이 필드를 ID 열이나 계산 열에서도 사용할 수 있습니다.|  
||||

 이러한 특성은 테이블 반환 매개 변수 열에 대해서만 유효하고 다른 매개 변수에 대해서는 무시됩니다.  
  
 SQL_CA_SS_COL_HAS_DEFAULT_VALUE가 테이블 반환 매개 변수 열에 대해 설정된 경우 해당 열의 SQL_DESC_DATA_PTR은 null 포인터여야 합니다. 그렇지 않은 경우 SQLExecute 또는 SQLExecDirect는 SQL_ERROR을 반환 합니다. SQLSTATE = 07S01 및 "매개 변수, 열에 대 한 기본 매개 변수 사용이 잘못 되었습니다" 라는 메시지가 포함 된 진단 레코드가 생성 됩니다 \<p> \<c> \<p> . 여기서은 매개 변수 서 수이 고는 \<c> 열 서 수입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
