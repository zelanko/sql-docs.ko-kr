---
title: 테이블 반환 매개 변수 설명자 필드 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13fb698d9a5be2e8fc949ad793cf19ac2aae97b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791871"
---
# <a name="table-valued-parameter-descriptor-fields"></a>테이블 반환 매개 변수 설명자 필드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  테이블 반환 매개 변수 지원에는 ODBC APD(응용 프로그램 매개 변수 설명자) 및 IPD(구현 매개 변수 설명자)의 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 필드가 포함되어 있습니다.  
  
## <a name="remarks"></a>Remarks  
  
|이름|위치|형식|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|테이블 반환 매개 변수의 서버 유형 이름입니다.<br /><br /> SQLBindParameter에 대 한 호출에서 테이블 반환 매개 변수 형식 이름을 지정 하면 항상 ANSI 응용 프로그램으로 작성 된 응용 프로그램에도 유니코드 값으로 지정 해야 합니다. 매개 변수에 사용 된 값 *StrLen_or_IndPtr* SQL_NTS 또는 문자열 길이의 sizeof(WCHAR) 곱한 이름 이어야 합니다.<br /><br /> 테이블 반환 매개 변수 형식 이름을 지정 된 경우 SQLSetDescField를 통해 응용 프로그램 방식으로 따르는 리터럴을 사용 하 여 지정할 수 있습니다 빌드됩니다. ODBC 드라이버 관리자에서 필요한 모든 유니코드 변환을 수행합니다.|  
|SQL_CA_SS_TYPE_CATALOG_NAME(읽기 전용)|IPD|SQLTCHAR*|유형이 정의된 카탈로그입니다.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|유형이 정의된 스키마입니다.|  
  
 응용 프로그램에서 테이블 반환 매개 변수에 대해 SQL_CA_SS_TYPE_CATALOG_NAME을 설정하면 안 됩니다. 이렇게 하면 SQL_ERROR가 반환되며 SQLSTATE = HY091 및 "잘못된 설명자 필드 식별자입니다"라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 매개 변수 포커스가 테이블 반환 매개 변수로 설정된 경우 다음 문 특성과 설명자 헤더 필드가 테이블 반환 매개 변수에 적용됩니다.  
  
|이름|위치|형식|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> APD의 SQL_DESC_ARRAY_SIZE와 같습니다.|APD|SQLUINTEGER|테이블 반환 매개 변수에 대한 버퍼 배열의 배열 크기입니다. 이 값은 버퍼에 포함될 최대 행 수이거나 행의 버퍼 크기입니다. 테이블 반환 매개 변수 값 자체는 버퍼에 포함될 수 있는 것보다 많거나 적은 행을 포함할 수 있습니다. 기본값은 1입니다.<br /><br /> 참고: SQL_SOPT_SS_PARAM_FOCUS가 기본값인 0으로 설정 하는 경우 SQL_ATTR_PARAMSET_SIZE는 문을 참조 및 매개 변수 집합 수를 지정 합니다. SQL_SOPT_SS_PARAM_FOCUS가 테이블 반환 매개 변수의 서수로 설정된 경우 테이블 반환 매개 변수를 참조하며 테이블 반환 매개 변수에 대해 매개 변수 집합당 행 수를 지정합니다.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|기본값은 SQL_PARAM_BIND_BY_COLUMN입니다.<br /><br /> 행 단위 바인딩을 선택하려면 이 필드를 테이블 반환 매개 변수 행 집합에 바인딩될 버퍼 인스턴스나 구조의 길이로 설정합니다. 이 길이에는 바인딩된 모든 열과 구조 또는 버퍼의 패딩에 대한 공간이 포함되어야 합니다. 이렇게 하면 바인딩된 열의 주소가 지정된 길이로 증가할 때 결과가 다음 행에 있는 동일한 열의 시작 부분을 가리킵니다. 사용 하는 경우는 **sizeof** ANSI c에서 연산자를이 동작이 유지 됩니다.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|기본값은 Null 포인터입니다.<br /><br /> 이 필드가 Null이 아니면 드라이버에서 포인터를 역참조하고, 설명자 레코드(SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR)의 각 지연된 필드에 역참조된 값을 추가하며, 새 포인터 값을 사용하여 데이터 값에 액세스합니다.|  
  
 이 필드는 테이블 반환 매개 변수에서만 유효하고 다른 데이터 형식에 대해서는 무시됩니다.  
  
 저장 프로시저 호출에서 SQL_CA_SS_TYPE_NAME은 옵션입니다. 서버에서 테이블 반환 매개 변수의 유형을 확인할 수 있게 하려면 프로시저 호출이 아닌 SQL 문에 대해 지정해야 합니다.  
  
 유형 이름이 필수이고 테이블 반환 매개 변수의 테이블 유형이 저장 프로시저와는 다른 스키마에 정의되어 있으면 IPD(구현 매개 변수 설명자)에 SQL_CA_SS_TYPE_SCHEMA_NAME을 지정해야 합니다. 그렇지 않으면 서버에서 테이블 반환 매개 변수의 유형을 확인할 수 없습니다. 이 SQLExecute 또는 SQLExecDirect를 호출 하는 경우는 오류가 발생 합니다. 오류에는 SQLSTATE= 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 포함됩니다.  
  
 테이블 반환 매개 변수 열은 행 단위 또는 열 단위 바인딩을 사용할 수 있습니다. 기본값은 열 단위 바인딩입니다. 행 단위 바인딩은 SQL_ATTR_PARAM_BIND_TYPE 및 SQL_ATTR_ PARAM_BIND_OFFSET_PTR을 설정하여 지정할 수 있습니다. 이는 열과 매개 변수의 행 단위 바인딩과 유사합니다.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME을 함께 사용하여 CLR 사용자 정의 형식 매개 변수와 연결된 카탈로그와 스키마를 검색할 수도 있습니다. 이러한 유형에 대한 기존의 유형별 카탈로그 스키마 특성 대신 이 카탈로그와 스키마를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
