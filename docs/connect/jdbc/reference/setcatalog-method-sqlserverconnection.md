---
description: setCatalog 메서드(SQLServerConnection)
title: setCatalog 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 655da723b4f3babb1cd3dd7a938f38382b4e93e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432335"
---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그 이름을 설정하여 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 데이터베이스 중 작업할 하위 공간을 선택합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 카탈로그 이름이 포함하는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setCatalog 메서드는 java.sql.Connection 인터페이스의 setCatalog 메서드에 의해 지정됩니다.  
  
 *catalog* 인수는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 의해 자동으로 이스케이프됩니다. 이 메서드를 사용하면 Connection 개체의 카탈로그 속성이 설정됩니다. 이 속성은 다른 방법으로 암시적으로 설정되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
