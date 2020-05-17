---
title: getClientInfo 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d3005e2b5ae8628ab31ceeb6314159afd796e83
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953133"
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
  
 검색할 클라이언트 정보 속성의 이름이 들어 있는 String입니다.  
  
## <a name="return-value"></a>Return Value  
 클라이언트 정보 속성의 값이 들어 있는 String입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getClientInfo 메서드는 java.sql.Connection 인터페이스의 getClientInfo 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 따라서 이 메서드는 **null**을 반환합니다.  
  
 마찬가지로 애플리케이션에서는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 클래스의 [getClientInfoProperties](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 메서드를 사용하여 드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색할 수 있습니다. [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드는 빈 결과 집합을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
