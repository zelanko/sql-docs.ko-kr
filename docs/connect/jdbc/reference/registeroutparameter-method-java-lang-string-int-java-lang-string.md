---
title: 형식 및 이름을 위한 registerOutParameter 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f962c912-2475-4e1f-a384-579be2d17f37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18c7dad22a4f5314a0bc920c650bcdf0ecd32d52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975923"
---
# <a name="registeroutparameter-method-javalangstring-int-javalangstring"></a>registerOutParameter 메서드(java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 이름의 OUT 매개 변수를 지정된 JDBC 형식 및 형식 이름으로 등록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n,  
                                 java.lang.String s1)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *s*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *n*  
  
 java.sql.Types에 정의된 JDBC 형식 코드입니다.  
  
 *s1*  
  
 정규화된 SQL 형식 이름이 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 registerOutParameter 메서드는 java. CallableStatement 인터페이스의 registerOutParameter 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [registerOutParameter 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
