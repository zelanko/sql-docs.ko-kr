---
title: "getClientInfo 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db4aac7f305f8c4e8dd14943975a65653cde68a8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 클라이언트 정보 속성의 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *name*  
  
 검색할 클라이언트 정보 속성의 이름을 포함 하는 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 클라이언트 정보 속성의 값을 포함 하는 문자열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getClientInfo 메서드는 java.sql.Connection 인터페이스의 getClientInfo 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 클라이언트 정보 속성을 지원 하지 않습니다. 이 메서드가 반환 하는 결과적으로, **null**합니다.  
  
 마찬가지로 응용 프로그램을 사용할 수는 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 의 메서드는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 드라이버에서 지 원하는 클라이언트 정보 속성의 목록을 검색 하는 클래스입니다. [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드는 빈 결과 집합을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getClientInfo 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
