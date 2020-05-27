---
title: getMaxRows 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0b9df5512466c5f12c5fda1b4e5cb4a91504499
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982075"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>Return Value  
 최대 행 수를 나타내는 **int**이며, 제한이 없는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMaxRows 메서드는 java.sql.Statement 인터페이스의 getMaxRows 메서드에 의해 지정됩니다.  
  
 동적 스크롤 가능 커서의 경우 이 getMaxRows 메서드는 항상 0을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
