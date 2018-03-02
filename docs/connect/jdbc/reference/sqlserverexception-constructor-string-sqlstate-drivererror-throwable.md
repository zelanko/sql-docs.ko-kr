---
title: "SQLServerException 생성자 (java.lang.String, SQLState, DriverError, java.lang.Throwable) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 101eca8f837dcbda00b252d5dc9867dfeb754351
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException 생성자 (java.lang.String, SQLState, DriverError, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  새 인스턴스를 초기화는 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 지정 되 면 클래스는 **문자열** 개체는 **sqlstate** 개체는 **drivererror** 개체 및 **throw 할 수 있는** 개체입니다.

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
  
 드라이버 오류 있는 열거형 개체입니다.
 
 *cause*  
  
 예외의 원인 있는 throw 할 수 있는 개체입니다.
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerException 생성자](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 클래스](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
