---
title: setClientInfo 메서드(java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 177b92c12ba9daa410de1e65cc3a38b8744f4149
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927166"
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
  
 설정할 클라이언트 정보 속성의 이름이 들어 있는 문자열입니다.  
  
 *value*  
  
 클라이언트 정보 속성에 설정할 값이 들어 있는 문자열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setClientInfo 메서드는 java.sql.Connection 인터페이스의 setClientInfo 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 2\.0 JDBC 드라이버에서 이 메서드는 속성에 대한 경고를 생성합니다. 애플리케이션에서는 [SQLServerConnection](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 클래스의 [getWarnings](../../../connect/jdbc/reference/sqlserverconnection-class.md) 메서드를 사용하여 경고를 검색해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
