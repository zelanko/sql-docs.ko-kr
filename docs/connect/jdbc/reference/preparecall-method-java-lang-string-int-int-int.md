---
title: prepareCall 메서드(java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80e4c2ba3c7e8d5624ca226703f7aeb48b8ac436
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923181"
---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall 메서드(java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 형식, 동시성 및 유지 기능을 사용하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체를 생성하는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **String**입니다.  
  
 *nType*  
  
 결과 집합 유형을 나타내는 **int**입니다.  
  
 *nConcur*  
  
 결과 집합 동시성 유형을 나타내는 **int**입니다.  
  
 *nHold*  
  
 결과 집합 유지 기능을 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 CallableStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 prepareCall 메서드는 java.sql.Connection 인터페이스의 prepareCall 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [prepareCall 메서드&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
