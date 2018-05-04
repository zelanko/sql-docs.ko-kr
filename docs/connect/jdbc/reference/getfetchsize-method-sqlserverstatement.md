---
title: getFetchSize 메서드 (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f27175ff8b83e6c60fbf7f92b7dcf8d37d3658c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize 메서드 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  집합 수를 검색 결과의 결과 집합에서 생성 된 개체에 대해 기본 인출 크기로 사용 되는 행 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 변수에 지정 된 인출 크기를 나타내는 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) 메서드.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getFetchSize 메서드는 java.sql.Statement 인터페이스의 getFetchSize 메서드가 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
