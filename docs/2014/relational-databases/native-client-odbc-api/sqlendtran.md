---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: rothja
ms.author: jroth
ms.openlocfilehash: e5d44756131b6133baec69e34da11055a965e2da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022733"
---
# <a name="sqlendtran"></a>SQLEndTran
  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서를 닫습니다. 서버 커서는 정적 상태가 될 때까지 닫힙니다. **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서의 동작은 [SQLSetConnectAttr](sqlsetconnectattr.md)을 통해 설정된, 드라이버 관련 ODBC 연결 특성인 SQL_COPT_SS_PRESERVE_CURSORS의 값에 의해 결정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 구현 세부 정보](odbc-api-implementation-details.md)   
 [SQLEndTran 함수(SQLEndTran Function)](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
