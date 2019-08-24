---
title: setClientInfo 메서드 () | Microsoft Docs
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
ms.openlocfilehash: a332f42c8193c851a33036af214ac31366986023
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974747"
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
 이 setClientInfo 메서드는 setClientInfo 인터페이스의 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 이 메서드는 *properties* 입력 매개 변수가 빈 속성 집합을 참조하지 않을 경우 경고를 생성합니다. 즉, 이 메서드는 애플리케이션에서 설정하려고 하는 속성에 대한 경고를 생성합니다. 애플리케이션에서는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) 메서드를 사용하여 각 경고를 검색해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
