---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a37821dff5176dfcb42cfd0a9f6424dfcc3f1938
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785699"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField를 사용 하 여 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열의 설명자 필드를 설정할 수 있습니다. 사용할 수 있는 필드에 대 한 자세한 내용은 테이블 반환 매개 변수 [설명자 필드](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) 및 [테이블 반환 매개 변수 구성 열의 설명자 필드](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)를 참조 하세요.  
  
## <a name="remarks"></a>주의  
 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 테이블 반환 매개 변수가 아닌 매개 변수의 서 수로 설정 하려고 하면 SQLSetStmtAttr가 SQL_ERROR를 반환 하 고 SQLSTATE = HY024 및 "잘못 된 특성 값입니다." 라는 메시지가 포함 된 진단 레코드가 생성 됩니다. SQL_SOPT_SS_PARAM_FOCUS는 SQL_ERROR가 반환될 때 변경되지 않습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 매개 변수의 설명자 레코드에 대한 액세스가 복원됩니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [테이블 반환 매개 &#40;변수 ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSetDescField 지원  
 ODBC에서 날짜/시간 기능이 향상되었습니다. 새로운 날짜/시간 형식에 제공되는 설명자 필드에 대한 자세한 내용은 [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)를 참조하십시오.  
  
 자세한 내용은 [ODBC&#41;의 날짜 및 시간 기능 향상 &#40;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSetDescField 지원  
 SQLSetDescField는 많은 CLR Udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC &#40;&#41;의 Large CLR 사용자 정의 형식](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>스파스 열에 대한 SQLSetDescField 지원  
 SQLSetDecField를 사용 하 여 APD (응용 프로그램 매개 변수 설명자)의 SQL_SOPT_SS_NAME_SCOPE SQL_SS_NAME_SCOPE_EXTENDED 값으로 설정 하 고 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 수 있습니다.  
  
 자세한 내용은 [스파스 열에서 ODBC &#40;&#41;지원](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
