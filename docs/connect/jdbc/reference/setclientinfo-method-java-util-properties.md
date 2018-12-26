---
title: setClientInfo 메서드 (java.util.Properties) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16e71bee35ab777ef8a19bb1ee92a9f9931da04d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813441"
---
# <a name="setclientinfo-method-javautilproperties"></a>setClientInfo 메서드(java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결의 클라이언트 정보 속성에 대한 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *properties*  
  
 설정할 클라이언트 정보 속성의 목록이 들어 있는 Properties 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setClientInfo 메서드는 java.sql.Connection 인터페이스의 setClientInfo 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 이 메서드는 *properties* 입력 매개 변수가 빈 속성 집합을 참조하지 않을 경우 경고를 생성합니다. 즉, 이 메서드는 응용 프로그램에서 설정하려고 하는 속성에 대한 경고를 생성합니다. 애플리케이션에서는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 메서드를 사용하여 각 경고를 검색해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
