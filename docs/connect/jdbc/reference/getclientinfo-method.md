---
description: getClientInfo 메서드()
title: getClientInfo 메서드() | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31c88ff13769c192c9fdc468cd21d2b3f2a12dbe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436685"
---
# <a name="getclientinfo-method-"></a>getClientInfo 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서 지원되는 각 클라이언트 정보 속성의 이름 및 현재 값이 들어 있는 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>Return Value  
 드라이버에서 지원되는 각 클라이언트 정보 속성의 이름 및 현재 값이 들어 있는 Properties 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getClientInfo 메서드는 java.sql.Connection 인터페이스의 getClientInfo 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 결과적으로 이 메서드는 빈 Properties 개체를 반환합니다.  
  
 마찬가지로 애플리케이션에서는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스의 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드를 사용하여 드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색할 수 있습니다. [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드는 빈 결과 집합을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
