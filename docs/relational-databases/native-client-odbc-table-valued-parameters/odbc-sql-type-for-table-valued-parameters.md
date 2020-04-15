---
title: 테이블 값 매개 변수에 대한 ODBC SQL 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6aae522544f4d9532dbc2d71db1b3d55ebee3da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297843"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>테이블 반환 매개 변수의 ODBC SQL 유형
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  새로운 ODBC SQL 형식인 SQL_SS_TABLE에서 테이블 반환 매개 변수에 대한 지원을 제공합니다.  
  
## <a name="remarks"></a>설명  
 SQL_SS_TABLE은 다른 ODBC 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수 없습니다.  
  
 SQL_SS_TABLE SQLBindParameter의 *ValueType* 매개 변수에서 C 데이터 유형으로 사용되거나 응용 프로그램 매개 변수 설명자(APD) 레코드에서 SQL_DESC_TYPE SQL_SS_TABLE 설정하려는 시도가 SQL_ERROR 반환되고 SQLSTATE=HY003, "잘못된 응용 프로그램 버퍼 유형"으로 진단 레코드가 생성됩니다.  
  
 IPD 레코드에 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정되어 있고 해당 APD 레코드가 SQL_C_DEFAULT가 아닌 경우 SQL_ERROR가 반환되고 SQLSTATE=HY003, "잘못된 애플리케이션 버퍼 형식입니다"가 표시되며 진단 레코드가 생성됩니다. 이 문제는 SQLSetDescField, SQLSetDescRec 또는 SQLBind매개 변수의 *매개 변수 유형에서* 발생할 수 있습니다.  
  
 SQLGetData를 호출할 때 *TargetType* 매개 변수가 SQL_SS_TABLE 경우 SQL_ERROR 반환되고 SQLSTATE=HY003, "잘못된 응용 프로그램 버퍼 유형"으로 진단 레코드가 생성됩니다.  
  
 테이블 반환 매개 변수 열은 SQL_SS_TABLE 형식으로 바인딩할 수 없습니다. **SQLBindParameter** 을 SQL_SS_TABLE로 설정하고 *ParameterType* 를 호출하면 SQL_ERROR가 반환되고 SQLSTATE=HY004, "잘못된 SQL 데이터 형식입니다"가 표시되며 진단 레코드가 생성됩니다. 이는 SQLSetDescField 및 SQLSetDescRec에서도 발생할 수 있습니다.  
  
 테이블 반환 매개 변수 열 값에는 매개 변수 및 결과 열과 동일한 데이터 변환 옵션이 포함됩니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 테이블 반환 매개 변수를 입력 매개 변수로만 사용할 수 있습니다. SQLBindParameter 또는 SQLSetDescField를 통해 SQL_PARAM_INPUT 이외의 값으로 SQL_DESC_PARAMETER_TYPE 설정하려고 하면 SQL_ERROR 반환되고 SQLSTATE=HY105 및 "잘못된 매개 변수 유형"이라는 메시지가 있는 명령문에 진단 레코드가 추가됩니다.  
  
 테이블 반환 매개 변수에는 행별 기본값이 지원되지 않으므로 테이블 반환 매개 변수 열의 *StrLen_or_IndPtr*에는 SQL_DEFAULT_PARAM을 사용할 수 없습니다. 대신 애플리케이션에서 열 특성 SQL_CA_SS_COL_HAS_DEFAULT_VALUE를 1로 설정할 수 있습니다. 즉, 해당 열이 모든 행에 대해 기본값을 갖습니다. *StrLen_or_IndPtr* SQL_DEFAULT_PARAM 설정하면 SQLExecute 또는 SQLExecDirect가 SQL_ERROR 반환하고 SQLSTATE=HY090 및 "잘못된 문자열 또는 버퍼 길이"라는 메시지가 있는 명령문에 진단 레코드가 추가됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 값 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
