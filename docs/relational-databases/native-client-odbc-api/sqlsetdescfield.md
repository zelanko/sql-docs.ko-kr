---
title: SQLSetDesc필드 | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f699610ce3aac1443439aa5d293e92104f3033d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292134"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField는 테이블 값 매개 변수 및 테이블 값 매개 변수 열에 대한 설명자 필드를 설정하는 데 사용할 수 있습니다. 사용 가능한 필드에 대한 자세한 내용은 [테이블 값 매개 변수 설명자 필드](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) 및 테이블 값 매개 변수 구성 [열에 대한 설명자 필드를](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)참조하십시오.  
  
## <a name="remarks"></a>설명  
 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 값 매개 변수가 아닌 매개 변수의 서수에 SQL_SOPT_SS_PARAM_FOCUS 설정하려고 하면 SQLSetStmtAttr이 SQL_ERROR 반환하고 SQLSTATE = HY024 및 "잘못된 특성 값"이라는 메시지로 진단 레코드가 만들어집니다. SQL_SOPT_SS_PARAM_FOCUS는 SQL_ERROR가 반환될 때 변경되지 않습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 매개 변수의 설명자 레코드에 대한 액세스가 복원됩니다.  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSetDescField 지원  
 ODBC에서 날짜/시간 기능이 향상되었습니다. 새로운 날짜/시간 형식에 제공되는 설명자 필드에 대한 자세한 내용은 [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)를 참조하십시오.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSetDescField 지원  
 SQLSetDescField는 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>스파스 열에 대한 SQLSetDescField 지원  
 SQLSetDecField는 응용 프로그램 매개 변수 설명자(APD)의 SQL_SOPT_SS_NAME_SCOPE SQL_SS_NAME_SCOPE_EXTENDED 및 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 값으로 설정하는 데 사용할 수 있습니다.  
  
 자세한 내용은 [희소 열 지원 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLSetDesc필드](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
