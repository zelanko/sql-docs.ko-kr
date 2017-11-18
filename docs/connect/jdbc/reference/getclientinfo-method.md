---
title: "getClientInfo 메서드 () | Microsoft Docs"
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
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed81345b9cf45678fd4571fca747eebb7fc30f9b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-"></a>getClientInfo 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서 지원되는 각 클라이언트 정보 속성의 이름 및 현재 값이 들어 있는 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>반환 값  
 이름 및 각 드라이버에서 지 원하는 클라이언트 정보 속성의 현재 값을 포함 하는 속성 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getClientInfo 메서드는 java.sql.Connection 인터페이스의 getClientInfo 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 클라이언트 정보 속성을 지원 하지 않습니다. 결과적으로,이 메서드는 빈 속성 개체를 반환합니다.  
  
 마찬가지로 응용 프로그램을 사용할 수는 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 의 메서드는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 드라이버에서 지 원하는 클라이언트 정보 속성의 목록을 검색 하는 클래스입니다. [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드는 빈 결과 집합을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getClientInfo 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

