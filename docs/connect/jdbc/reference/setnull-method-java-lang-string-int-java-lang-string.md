---
description: setNull 메서드(java.lang.String, int, java.lang.String)
title: setNull 메서드(java.lang.String, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c4d7666b4b743428ce2f81c7d84cd3b7caeca47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458625"
---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>setNull 메서드(java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정할 매개 변수의 형식 및 이름이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **String**입니다.  
  
 *nType*  
  
 java.sql.Types에 의해 정의된 JDBC 형식 코드입니다.  
  
 *sTypeName*  
  
 설정할 매개 변수의 정규화된 이름을 나타내는 **String**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setNull 메서드는 java.sql.CallableStatement 인터페이스의 setNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNull 메서드(SQLServerCallableStatement)](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
