---
title: 날짜 및 일정에 대한 setDate 메서드 - string | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42562914e8c99debbc9423c8a5d63cd921779c4a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926664"
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
  
 Calendar 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setDate 메서드는 java.sql.CallableStatement 인터페이스의 setDate 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
