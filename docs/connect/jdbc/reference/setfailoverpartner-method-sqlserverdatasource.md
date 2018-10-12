---
title: setFailoverPartner 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b737bee1f97e11a1acf0adf039603125b15609c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622001"
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *serverName*  
  
 장애 조치(Failover) 서버의 이름이 들어 있는 **String**입니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드에서 설정한 값은 주 서버에 대한 초기 연결이 실패할 경우에 사용되며, 초기 연결이 만들어진 후에는 이 값이 무시됩니다. 또한 [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) 메서드를 이 메서드와 함께 사용해야 합니다. 그렇지 않으면 예외가 발생합니다.  
  
 드라이버에서는 장애 조치(Failover) 서버의 이름이 설정된 경우 장애 조치(Failover) 서버의 포트 번호를 지정할 수 없습니다. 그러나 [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 메서드와 함께 [setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) 메서드 및 [setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) 메서드를 호출할 수는 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
