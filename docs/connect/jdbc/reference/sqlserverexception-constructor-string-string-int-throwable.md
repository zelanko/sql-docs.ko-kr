---
title: SQLServerException 생성자(java.lang.String, java.lang.String, int, java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18827d05bc5567b4566eaa006d88c249874132cf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971081"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 생성자(java.lang.String, java.lang.String, int, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **문자열** 개체, **문자열** 개체, **int** 및 **throwable** 개체가 지정된 경우 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 클래스의 새 인스턴스를 초기화합니다.

## <a name="syntax"></a>구문  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>매개 변수  
 *errText*  
  
 오류 문자를 포함하는 문자열입니다.
  
 *errState*  
  
 오류의 상태를 포함하는 문자열입니다.
 
 *errNum*  
  
 예외의 오류 코드를 포함하는 int입니다.
 
 *cause*  
  
 예외의 원인을 포함하는 throwable 개체입니다.
  
## <a name="see-also"></a>참고 항목  
 [SQLServerException 생성자](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 클래스](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
