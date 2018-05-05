---
title: 테이블 반환 매개 변수의 ODBC SQL 유형 | Microsoft Docs
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
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cbf2b434d29033961608494478bc775946226ced
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>테이블 반환 매개 변수의 ODBC SQL 유형
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  새로운 ODBC SQL 형식인 SQL_SS_TABLE에서 테이블 반환 매개 변수에 대한 지원을 제공합니다.  
  
## <a name="remarks"></a>주의  
 SQL_SS_TABLE은 다른 ODBC 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수 없습니다.  
  
 SQL_SS_TABLE에서 C 데이터 형식으로 사용 되는 경우는 *ValueType* SQL_DESC_TYPE을 SQL_SS_TABLE로는 응용 프로그램 매개 변수 APD (설명자) 레코드의 설정에 대 한 SQLBindParameter 또는 시도가 매개 변수에 이루어지면 SQL_ERROR가 반환 되 고 진단 레코드가 생성은 SQLSTATE = HY003, "잘못 된 응용 프로그램 버퍼 형식 입니다" 합니다.  
  
 IPD 레코드에 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정되어 있고 해당 APD 레코드가 SQL_C_DEFAULT가 아닌 경우 SQL_ERROR가 반환되고 SQLSTATE=HY003, "잘못된 응용 프로그램 버퍼 형식입니다"가 표시되며 진단 레코드가 생성됩니다. 이 발생할 수 있습니다는 *ParameterType* SQLSetDescField, SQLSetDescRec 또는 SQLBindParameter의 합니다.  
  
 경우는 *TargetType* SQLGetData를 호출할 때 매개 변수가 SQL_SS_TABLE을이 아니면 SQL_ERROR가 반환 되 고 SQLSTATE 된 진단 레코드가 생성 됩니다 = HY003, "잘못 된 응용 프로그램 버퍼 형식 입니다"입니다.  
  
 테이블 반환 매개 변수 열은 SQL_SS_TABLE 형식으로 바인딩할 수 없습니다. **SQLBindParameter** 을 SQL_SS_TABLE로 설정하고 *ParameterType* 를 호출하면 SQL_ERROR가 반환되고 SQLSTATE=HY004, "잘못된 SQL 데이터 형식입니다"가 표시되며 진단 레코드가 생성됩니다. SQLSetDescRec SQLSetDescField와도 발생할 수 있습니다.  
  
 테이블 반환 매개 변수 열 값에는 매개 변수 및 결과 열과 동일한 데이터 변환 옵션이 포함됩니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 테이블 반환 매개 변수를 입력 매개 변수로만 사용할 수 있습니다. Desc_parameter_type SQLBindParameter 또는 SQLSetDescField 통해 SQL_PARAM_INPUT 이외의 값으로 설정 하려고 시도, SQL_ERROR가 반환 되 고 진단 레코드가 sqlstate 문에 추가 = HY105 및 "잘못 된 매개 변수 메시지 "을 입력 합니다.  
  
 테이블 반환 매개 변수에는 행별 기본값이 지원되지 않으므로 테이블 반환 매개 변수 열의 *StrLen_or_IndPtr*에는 SQL_DEFAULT_PARAM을 사용할 수 없습니다. 대신 응용 프로그램에서 열 특성 SQL_CA_SS_COL_HAS_DEFAULT_VALUE를 1로 설정할 수 있습니다. 즉, 해당 열이 모든 행에 대해 기본값을 갖습니다. 경우 *StrLen_or_IndPtr* 설정 되어를 SQL_DEFAULT_PARAM으로 SQLExecute 또는 SQLExecDirect에서 SQL_ERROR를 반환 하 고 진단 레코드가 sqlstate 문을에 추가할 = HY090 및 "잘못 된 문자열 또는 버퍼 길이" 메시지입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
