---
title: setCatalog 메서드 (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91597c7a995fb0ecf810d3b0f58760c12784564e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842208"
---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이러한 하위 네임 스페이스를 선택 하는 데 주어진된 카탈로그 이름을 설정 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 작업 하려는 개체의 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setCatalog 메서드는 java.sql.Connection 인터페이스의 setCatalog 메서드에 의해 지정 됩니다.  
  
 *카탈로그* 인수에 의해 이스케이프 되는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 자동으로 합니다. 이 메서드를 사용 하 여 연결 개체에 대 한 카탈로그 속성을 설정 합니다. 이 속성은 다른 방법으로 암시적으로 설정되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
