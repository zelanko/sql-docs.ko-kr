---
title: "SQLTransact 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLTransact
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLTransact
helpviewer_keywords: SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e293ad391bee9698941b8681a852ed75bf0717e8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqltransact-function"></a>SQLTransact 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 Odbc 3. *x*, ODBC 2*.x* 함수 **SQLTransact** 로 대체 되었습니다 **SQLEndTran**합니다. 자세한 내용은 참조 [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLTransact**합니다. 응용 프로그램 연결 핸들에는 비동기 작업을 사용 하 여 사용 해야 **SQLEndTran**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
