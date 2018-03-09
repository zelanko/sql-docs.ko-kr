---
title: "setClientInfo 메서드 (java.lang.String, java.lang.String) | Microsoft Docs"
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
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e136cd3eb2330bfd82c531acaa37838ed30e7713
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>setClientInfo 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 클라이언트 정보 속성의 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *name*  
  
 설정할 클라이언트 정보 속성의 이름을 포함 하는 문자열입니다.  
  
 *value*  
  
 클라이언트 정보 속성을 설정 하는 값을 포함 하는 문자열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setClientInfo 메서드는 java.sql.Connection 인터페이스의 setClientInfo 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 클라이언트 정보 속성을 지원 하지 않습니다. 2.0 JDBC 드라이버에서 이 메서드는 속성에 대한 경고를 생성합니다. 응용 프로그램 사용 해야 [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스 경고를 검색 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setClientInfo 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
