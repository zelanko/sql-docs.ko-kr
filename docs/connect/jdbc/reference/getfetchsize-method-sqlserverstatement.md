---
title: "getFetchSize 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: efb6e1aca84c36afbfb761813ae8ab0efdfd2501
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
  

