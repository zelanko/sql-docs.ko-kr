---
title: prepareCall 메서드(java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6df80276995f7a58d51f4e1ea52539ab9eb6a66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597601"
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall 메서드(java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 형식 및 동시성을 사용하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 생성하는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **String**입니다.  
  
 *resultSetType*  
  
 결과 집합 유형을 나타내는 **int**입니다.  
  
 *resultSetConcurrency*  
  
 결과 집합 동시성 유형을 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 CallableStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 prepareCall 메서드는 java.sql.Connection 인터페이스의 prepareCall 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [prepareCall 메서드&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
