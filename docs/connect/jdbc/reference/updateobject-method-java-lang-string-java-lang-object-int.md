---
description: updateObject 메서드(java.lang.String, java.lang.Object, int)
title: updateObject 메서드(java.lang.String, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 27283ce1-637e-4e2c-91ee-8ad379114ac5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbc070f71830113875add1d4711671832ae4de12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478301"
---
# <a name="updateobject-method-javalangstring-javalangobject-int"></a>updateObject 메서드(java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 이름과 소수 자릿수가 지정된 경우 지정된 열을 **Object** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *obj*  
  
 **Object** 값입니다.  
  
 *scale*  
  
 java.sql.Types.DECIMAL 또는 java.sql.Types.NUMERIC 형식의 경우, 소수점 뒤의 자릿수입니다. 다른 모든 형식의 경우에는 이 값이 무시됩니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateObject 메서드는 java.sql.ResultSet 인터페이스의 updateObject 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateObject 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
