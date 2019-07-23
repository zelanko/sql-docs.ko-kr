---
title: setQueryTimeout 메서드 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a4a271e07dea5a533dcb19b098a3e3de29e535e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973185"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>setQueryTimeout 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  드라이버에서 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체가 실행될 때까지 대기하는 시간(초)을 지정된 시간(초)으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *초*  
  
 대기 시간(초)를 나타내는 **int**이며, 제한이 없는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setQueryTimeout 메서드는 setQueryTimeout 인터페이스의 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
