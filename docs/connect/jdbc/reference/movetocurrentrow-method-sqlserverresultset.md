---
title: "moveToCurrentRow 메서드 (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.moveToCurrentRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a7c754c-2d72-4207-b3bd-2afc6047fb3d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8548c196214955e03a04a9a318a30701b0b26f1e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# moveToCurrentRow 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 저장된 커서 위치(대개 현재 행)로 이동합니다.  
  
## 구문  
  
```  
  
public void moveToCurrentRow()  
```  
  
## 예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## 주의  
 이 moveToCurrentRow 메서드는 java.sql.ResultSet 인터페이스의 moveToCurrentRow 메서드에 의해 지정 됩니다.  
  
 커서가 삽입 행에 있지 않으면 이 메서드는 아무 영향도 주지 않습니다.  
  
## 관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

