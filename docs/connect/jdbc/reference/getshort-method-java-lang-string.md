---
title: "getShort 메서드 (java.lang.String) | Microsoft Docs"
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
- SQLServerCallableStatement.getShort (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cd39ed03-b3e8-443d-9c7a-e8cf2581e581
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76d7264024dacecf2e0548f482bf1a9f53dd8aed
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getshort-method-javalangstring"></a>getShort 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  로 지정된 된 매개 변수의 값을 검색 하는 **짧은** java 프로그래밍 언어 매개 변수 이름이 지정 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public short getShort(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **짧은** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getShort 메서드는 java.sql.CallableStatement 인터페이스의 getShort 메서드에 의해 지정 됩니다.  
  
 이 메서드는 에서만 지원 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] smallint, tinyint 및 bit와 같이 정수 값을 안전 하 게 반환할 수 있는 데이터 형식입니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getShort 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

