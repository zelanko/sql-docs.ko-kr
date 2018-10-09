---
title: setDate 메서드를 날짜 및 달력-문자열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDate (java.lang.String, java.sql.Date, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fd152ad6-dd5e-49ef-b166-917371a2cba6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9606d55aed9685563209b14680196e9acb570868
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743511"
---
# <a name="setdate-method-javalangstring-javasqldate-javautilcalendar"></a>setDate 메서드(java.lang.String, java.sql.Date, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 날짜 및 달력 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setDate(java.lang.String sCol,  
                    java.sql.Date x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 Date 개체입니다.  
  
 *c*  
  
 일정 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getDate 메서드는 java.sql.CallableStatement 인터페이스의 getDate 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
