---
description: unwrap 메서드(SQLServerPreparedStatement)
title: unwrap 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1ac875841272b339738245c6bd7ca09cf757c5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458085"
---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>unwrap 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 인터페이스를 정의하는 **T** 형식의 클래스입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 인터페이스를 구현하는 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) 메서드는 JDBC 4.0 사양에서 도입된 java.sql.Wrapper 인터페이스에 의해 정의됩니다.  
  
 애플리케이션에서는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]와 관련된 JDBC API에 대한 확장에 액세스해야 할 수 있습니다. unwrap 메서드는 이 개체가 확장하는 공용 클래스에서 공급업체 확장을 노출하는 경우 이 클래스에 대한 래핑 해제를 지원합니다.  
  
 이 메서드가 호출되면 개체가 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 및 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스로 래핑 해제합니다.  
  
 예제 코드는 [unwrap 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)를 참조하세요.  
  
 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [isWrapperFor 메서드(SQLServerPreparedStatement)](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
