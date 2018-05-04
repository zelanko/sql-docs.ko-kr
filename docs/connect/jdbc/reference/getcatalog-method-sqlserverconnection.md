---
title: getCatalog 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cc3aedba38d3ade6d08e1829d5970c2585cb1b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 카탈로그 이름을 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getCatalog 메서드는 java.sql.Connection 인터페이스의 getCatalog 메서드에 의해 지정 됩니다.  
  
 속성이 설정 되지 않은 경우에 SQLServerConnection 개체 또는 null의 현재 카탈로그 속성을 반환 합니다. 카탈로그 속성으로 명시적으로 설정 된는 [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) 메서드, 또는 참조에 대 한 현재 카탈로그의 TDS에 대 한 환경 변경 하 여 암시적으로 업데이트 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
