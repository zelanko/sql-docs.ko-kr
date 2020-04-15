---
title: SQLTransact 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a4f1da36a7c233e9a1b5832ee83e86a5c1f77d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287083"
---
# <a name="sqltransact-function"></a>SQLTransact 함수
**규칙**  
 버전 도입: ODBC 1.0 표준 규정 준수: 더 이상 사용되지 않는  
  
 **요약**  
 ODBC *3.x에서*ODBC *2.x* 함수 **SQLTransact가** **SQLEndTran으로**대체되었습니다. 자세한 내용은 [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)을 참조하십시오.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성은 **SQLTransact에서**지원되지 않습니다. 연결 핸들에서 비동기 연산을 사용하는 응용 프로그램은 **SQLEndTran**을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
