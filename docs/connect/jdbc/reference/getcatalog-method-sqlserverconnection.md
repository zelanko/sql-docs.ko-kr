---
title: getCatalog 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 482bf8e2928e423f326369223bd2148306712b39
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921560"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 현재 카탈로그 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>Return Value  
 카탈로그 이름이 포함하는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getCatalog 메서드는 java.sql.Connection 인터페이스의 getCatalog 메서드에 의해 지정됩니다.  
  
 SQLServerConnection 개체의 현재 카탈로그 속성을 반환하거나, 이 속성이 설정되지 않은 경우 null을 반환합니다. 카탈로그 속성은 [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) 메서드를 사용하여 명시적으로 설정되거나, 현재 카탈로그의 TDS에 대한 환경 변경 내용을 읽을 때 암시적으로 업데이트됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
