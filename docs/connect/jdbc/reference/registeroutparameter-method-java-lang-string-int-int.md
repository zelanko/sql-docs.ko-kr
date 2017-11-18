---
title: "registerOutParameter 메서드를 형식 및 소수 자릿수로 | Microsoft Docs"
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
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bddc557-4526-4843-9804-05dc83c8832d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 341300744a1a3643e6ac0cbbcb22d36c573de32b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="registeroutparameter-method-javalangstring-int-int"></a>registerOutParameter 메서드(java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 이름의 OUT 매개 변수를 지정된 JDBC 형식 및 소수 자릿수로 등록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n,  
                                 int n1)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *s*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *sqlType*  
  
 java.sql.Types에 정의된 JDBC 형식 코드입니다.  
  
 *소수 자릿수*  
  
 **int** 자릿수는 소수점 오른쪽에 올 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 registerOutParameter 메서드는 java.sql.CallableStatement 인터페이스의 registerOutParameter 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [registerOutParameter 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

