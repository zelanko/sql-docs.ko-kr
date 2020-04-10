---
title: createStatement 메서드(int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e260135aa251012edfa98a08d4db3c358c17c51
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927665"
---
# <a name="createstatement-method-int-int"></a>createStatement 메서드(int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 형식 및 동시성을 사용하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 생성하는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *resultSetType*  
  
 결과 집합 유형을 나타내는 **int** 값입니다.  
  
 *resultSetConcurrency*  
  
 결과 집합 동시성 유형을 나타내는 **int** 값입니다.  
  
## <a name="return-value"></a>Return Value  
 Statement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 createStatement 메서드는 java.sql.Connection 인터페이스의 createStatement 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [createStatement 메서드(SQLServerConnection)](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
