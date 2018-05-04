---
title: createStatement 메서드 (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cabeeaf2759991bda02b3dd1f59e247c7037f15
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="createstatement-method-int-int-int"></a>createStatement 메서드(int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 생성 하는 개체 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 지정 된 형식, 동시성 및 유지 기능을 사용 하 여 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *resultSetType*  
  
 **int** 결과 나타내는 값 유형을 설정 합니다.  
  
 *nConcur*  
  
 **int** 집합 동시성 유형을 결과 나타내는 값입니다.  
  
 *nHold*  
  
 **int** 유지 기능을 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 문 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 createStatement 메서드는 java.sql.Connection 인터페이스의 createStatement 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [createStatement 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
