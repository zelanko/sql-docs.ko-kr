---
title: getClientInfo 메서드 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6b68caa4abff00f113176791d06c6361c5da1e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953110"
---
# <a name="getclientinfo-method-"></a>getClientInfo 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서 지원되는 각 클라이언트 정보 속성의 이름 및 현재 값이 들어 있는 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>반환 값  
 드라이버에서 지원되는 각 클라이언트 정보 속성의 이름 및 현재 값이 들어 있는 Properties 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getClientInfo 메서드는 getClientInfo 인터페이스의 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 클라이언트 정보 속성을 지원하지 않습니다. 결과적으로이 메서드는 빈 속성 개체를 반환 합니다.  
  
 마찬가지로 애플리케이션에서는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스의 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드를 사용하여 드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색할 수 있습니다. [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 메서드는 빈 결과 집합을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getClientInfo 메서드(SQLServerConnection)](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
