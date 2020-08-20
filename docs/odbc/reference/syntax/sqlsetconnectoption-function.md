---
description: SQLSetConnectOption 함수
title: SQLSetConnectOption 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectOption
helpviewer_keywords:
- SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebe9166ea52971812e8905399da4ea0e6347361a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499535"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 ODBC*3.x에서 odbc*2.0 함수 **SQLSetConnectOption** 는 **SQLSetConnectAttr**로 대체 되었습니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)을 참조하세요.  
  
> [!NOTE]
>  ODBC*2.x 응용 프로그램이* odbc*3.x 드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)"을 참조 하십시오.  
  
## <a name="remarks"></a>설명  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성은 **SQLSetConnectOption**에서 지원 되지 않습니다. 연결 핸들에 대해 비동기 작업을 사용 하는 응용 프로그램은 **SQLSetConnectAttr**를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
