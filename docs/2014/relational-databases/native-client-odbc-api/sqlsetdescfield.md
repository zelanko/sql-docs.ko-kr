---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f65c26e1c6b9588b770acf1a66409dfde8ea1072
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188679"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField는 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열의 설명자 필드 설정에 사용할 수 있습니다. 사용 가능한 필드에 대 한 정보를 참조 하세요 [테이블 반환 매개 변수 설명자 필드](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) 하 고 [테이블 반환 매개 변수 구성 열의 설명자 필드](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)합니다.  
  
## <a name="remarks"></a>Remarks  
 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 반환 매개 변수가 아닌 매개 변수의 서 수에 SQL_SOPT_SS_PARAM_FOCUS를 설정 하려고 시도 SQLSetStmtAttr SQL_ERROR를 반환 하 고 sqlstate 진단 레코드가 생성 됩니다 = HY024 및 "잘못 된 특성 값이"입니다. SQL_SOPT_SS_PARAM_FOCUS는 SQL_ERROR가 반환될 때 변경되지 않습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 매개 변수의 설명자 레코드에 대한 액세스가 복원됩니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSetDescField 지원  
 ODBC에서 날짜/시간 기능이 향상되었습니다. 새로운 날짜/시간 형식에 제공되는 설명자 필드에 대한 자세한 내용은 [Parameter and Result Metadata](../native-client-odbc-date-time/metadata-parameter-and-result.md)를 참조하십시오.  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSetDescField 지원  
 SQLSetDescField는 큰 CLR 사용자 정의 형식 (Udt)을 지원합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>스파스 열에 대한 SQLSetDescField 지원  
 SQLSetDecField는 SQL_SOPT_SS_NAME_SCOPE를 SQL_SS_NAME_SCOPE_EXTENDED 및 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 값으로 응용 프로그램 매개 변수 설명자 (APD) 설정에 사용할 수 있습니다.  
  
 자세한 내용은 [Sparse Columns Support &#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
