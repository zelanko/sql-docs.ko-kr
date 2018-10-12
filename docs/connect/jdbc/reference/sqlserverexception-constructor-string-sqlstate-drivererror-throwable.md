---
title: SQLServerException 생성자 (java.lang.String, SQLState, DriverError, java.lang.Throwable) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: dc7608582a5ed146b656d41714853ba4c3b21b00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679981"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException 생성자 (java.lang.String, SQLState, DriverError, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  새 인스턴스를 초기화 합니다 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 주어 지 면 클래스는 **문자열** 개체를 **sqlstate** 개체를 **drivererror** 개체와 **throw 할 수 있는** 개체입니다.

## <a name="syntax"></a>구문  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>매개 변수  
 *errText*  
  
 오류 텍스트를 포함 하는 문자열입니다.
  
 *sqlState*  
  
 SQL 상태를 유지 하는 열거형 개체입니다.
 
 *driverError*  
  
 드라이버 오류를 포함 하는 열거형 개체입니다.
 
 *cause*  
  
 예외의 원인을 포함 하는 throw 할 수 있는 개체입니다.
  
## <a name="see-also"></a>참고 항목  
 [SQLServerException 생성자](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 클래스](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
