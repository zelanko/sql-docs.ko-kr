---
title: SQLTransact 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b76b7a550211522c2b2100776b88f311abb2b932
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646861"
---
# <a name="sqltransact-function"></a>SQLTransact 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 Odbc 3. *x*, ODBC 2 *.x* 함수 **SQLTransact** 바뀌었습니다 **SQLEndTran**합니다. 자세한 내용은 [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된, SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLTransact**합니다. 연결 핸들의 비동기 작업을 사용 하 여 응용 프로그램을 사용 해야 합니다 **SQLEndTran**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
