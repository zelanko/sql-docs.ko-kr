---
description: SQLGetConnectOption 함수
title: SQLGetConnectOption 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3fd7dc9a024348c4371fabdbcabfab63a6f071
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421287"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 *Odbc 3.x에서 odbc 2.x*함수 **SQLGetConnectOption** 는 **SQLGetConnectAttr**로 대체 *되었습니다.* 자세한 내용은 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)를 참조 하세요.  
  
> [!NOTE]
>  ODBC *2.x 응용 프로그램에서 odbc 2.x* *드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 을 참조 하세요.  
> 
> [!NOTE]
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성은 **SQLGetConnectOption**에서 지원 되지 않습니다. 연결 핸들에 대해 비동기 작업을 사용 하는 응용 프로그램은 **SQLGetConnectAttr**를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
