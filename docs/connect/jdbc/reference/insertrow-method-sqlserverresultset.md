---
description: insertRow 메서드(SQLServerResultSet)
title: insertRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a399b5dbcd9d4c330c79d73b3cb2a57b2e02675
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433685"
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 해당 데이터베이스에 삽입 행의 내용을 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 insertRow 메서드는 java.sql.ResultSet 인터페이스의 insertRow 메서드에 의해 지정됩니다.  
  
 이 메서드를 호출할 때 커서는 삽입 행에 있어야 합니다. 이 메서드를 호출한 후 커서는 삽입 행에 계속 있으며 결과 집합도 삽입 모드에 계속 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
