---
title: 테이블 반환 매개 변수의 ODBC SQL 유형 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de2c1a2b101775a3a7e97ecd4d89e32aefc4d3c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648407"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>테이블 반환 매개 변수의 ODBC SQL 유형
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  새로운 ODBC SQL 형식인 SQL_SS_TABLE에서 테이블 반환 매개 변수에 대한 지원을 제공합니다.  
  
## <a name="remarks"></a>Remarks  
 SQL_SS_TABLE은 다른 ODBC 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수 없습니다.  
  
 SQL_SS_TABLE의 C 데이터 형식으로 사용 됩니다는 *ValueType* SQLBindParameter, 또는 시도가 매개 변수에 SQL_SS_TABLE로 응용 프로그램 매개 변수 설명자 (APD) 레코드의 SQL_DESC_TYPE을 설정 하려고 하면 SQL_ERROR가 반환 되 고 진단 레코드가 생성 됩니다 HY003, = "잘못 된 응용 프로그램 버퍼 형식 입니다".  
  
 IPD 레코드에 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정되어 있고 해당 APD 레코드가 SQL_C_DEFAULT가 아닌 경우 SQL_ERROR가 반환되고 SQLSTATE=HY003, "잘못된 애플리케이션 버퍼 형식입니다"가 표시되며 진단 레코드가 생성됩니다. 이 발생할 수 있습니다 합니다 *ParameterType* SQLSetDescField, SQLSetDescRec 또는 SQLBindParameter의 합니다.  
  
 경우는 *TargetType* 매개 변수가 인 SQL_SS_TABLE SQLGetData 호출 하면 SQL_ERROR가 반환 되 고 진단 레코드가 생성 됩니다 HY003, = "잘못 된 응용 프로그램 버퍼 형식 입니다".  
  
 테이블 반환 매개 변수 열은 SQL_SS_TABLE 형식으로 바인딩할 수 없습니다. **SQLBindParameter** 을 SQL_SS_TABLE로 설정하고 *ParameterType* 를 호출하면 SQL_ERROR가 반환되고 SQLSTATE=HY004, "잘못된 SQL 데이터 형식입니다"가 표시되며 진단 레코드가 생성됩니다. SQLSetDescField 및 SQLSetDescRec 발생할 수 있습니다.  
  
 테이블 반환 매개 변수 열 값에는 매개 변수 및 결과 열과 동일한 데이터 변환 옵션이 포함됩니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 테이블 반환 매개 변수를 입력 매개 변수로만 사용할 수 있습니다. SQLBindParameter 또는 SQLSetDescField 통해 SQL_PARAM_INPUT 이외의 값으로 설정 하려고 하면 SQL_ERROR가 반환 하 고 진단 레코드가 문에 추가할 경우 = HY105 및 "잘못 된 매개 변수 메시지 "을 입력 합니다.  
  
 테이블 반환 매개 변수에는 행별 기본값이 지원되지 않으므로 테이블 반환 매개 변수 열의 *StrLen_or_IndPtr*에는 SQL_DEFAULT_PARAM을 사용할 수 없습니다. 대신 애플리케이션에서 열 특성 SQL_CA_SS_COL_HAS_DEFAULT_VALUE를 1로 설정할 수 있습니다. 즉, 해당 열이 모든 행에 대해 기본값을 갖습니다. 하는 경우 *StrLen_or_IndPtr* 설정할지를 SQL_DEFAULT_PARAM으로 SQLExecute 또는 SQLExecDirect에서 SQL_ERROR를 반환 하 고 진단 레코드가 문에 추가할 수는 HY090 및 "잘못 된 문자열 또는 버퍼 길이"입니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
