---
description: createStatement 메서드(int, int, int)
title: createStatement 메서드(int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53395cc630c161c15e50559fd1cc78b8faf5c044
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437945"
---
# <a name="createstatement-method-int-int-int"></a>createStatement 메서드(int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 형식, 동시성 및 유지 기능을 사용하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 생성하는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *resultSetType*  
  
 결과 집합 형식을 나타내는 **int**값입니다.  
  
 *nConcur*  
  
 결과 집합 동시성 형식을 나타내는 **int** 값입니다.  
  
 *nHold*  
  
 유지 기능을 나타내는 **int** 값입니다.  
  
## <a name="return-value"></a>반환 값  
 Statement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 createStatement 메서드는 java.sql.Connection 인터페이스의 createStatement 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [createStatement 메서드(SQLServerConnection)](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
