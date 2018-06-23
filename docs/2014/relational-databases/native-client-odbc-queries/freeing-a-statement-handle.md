---
title: 문 핸들 해제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7da2fec15303e9c2d50fb7aa2e6dc40266a380d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173100"
---
# <a name="freeing-a-statement-handle"></a>문 핸들 해제
  문 핸들을 다시 사용하는 것이 문 핸들을 삭제한 다음 새로 할당하는 것보다 더 효율적입니다. 따라서 문 핸들에 대해 새 SQL 문을 실행하기 전에 응용 프로그램에서 현재 문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 매개 변수 및 결과 호출 하 여 이전 SQL 문의 해야 바인딩 해제에 대 한 설정 하는 일반적으로 [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 및 SQL_UNBIND 옵션 및 다음 새 SQL 문에 대 한 다시 바인딩해야 합니다.  
  
 호출 응용 프로그램에서 문을 사용 하 여 완료 되 면 [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) 를 해당 문을 해제 합니다. **SQLDisconnect** 자동으로 연결 된 모든 문을 해제 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  