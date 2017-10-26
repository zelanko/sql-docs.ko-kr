---
title: "unwrap 메서드 (SQLServerPreparedStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85f008a4cf1135b1a0978d98bade8d2c99030629
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>unwrap 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  에 대 한 액세스를 허용 하도록 지정된 된 인터페이스를 구현 하는 개체를 반환 합니다.는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 형식의 클래스 **T** 인터페이스를 정의 합니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 인터페이스를 구현하는 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) 메서드는 JDBC 4.0 사양에서 도입 된 java.sql.Wrapper 인터페이스에 의해 정의 됩니다.  
  
 응용 프로그램에 관련 된 JDBC API에 대 한 확장에 액세스 해야 할 수는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. Unwrap 메서드는 공급 업체 확장 노출 하는 경우이 개체가 확장 하는 공용 클래스에 래핑 해제를 지원 합니다.  
  
 이 메서드가 호출 되 면 개체는 다음과 같은 클래스가 래핑 해제: [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 및 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)합니다.  
  
 예를 들어 코드 참조, [unwrap 메서드 &#40; SQLServerCallableStatement &#41; ](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [isWrapperFor 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

