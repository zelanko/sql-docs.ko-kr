---
title: "setCatalog 메서드 (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b766c76132bad3f66de98b431ee09d39753c40ab
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이러한 하위 네임 스페이스를 선택 하는 데 주어진된 카탈로그 이름을 설정 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 작업 하려는 개체의 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *카탈로그*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setCatalog 메서드는 java.sql.Connection 인터페이스의 setCatalog 메서드에 의해 지정 됩니다.  
  
 *카탈로그* 인수에 의해 이스케이프 되는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 자동으로 합니다. 이 메서드를 사용 하 여 연결 개체에 대 한 카탈로그 속성을 설정 합니다. 이 속성은 다른 방법으로 암시적으로 설정되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

