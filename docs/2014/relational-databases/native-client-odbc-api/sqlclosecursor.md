---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: rothja
ms.author: jroth
ms.openlocfilehash: 770a67432868516e5023d1cf0ff819501b4c130e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022875"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** 는 [SQLFreeStmt](sqlfreestmt.md) 를 SQL_CLOSE의 *옵션* 값으로 바꿉니다. **SQLCloseCursor**를 수신한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 보류 중인 결과 집합 행을 무시합니다. 문의 열 및 매개 변수 바인딩(있는 경우)은 **SQLCloseCursor**에 의해 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
