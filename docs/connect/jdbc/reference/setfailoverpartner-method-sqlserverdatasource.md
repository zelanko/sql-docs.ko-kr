---
title: setFailoverPartner 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf1c29750ef93d131e39616b2cd2d3059c8dd9b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *서버 이름*  
  
 A **문자열** 장애 조치 서버 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 이 메서드에서 설정한 값은 주 서버에 대한 초기 연결이 실패할 경우에 사용되며, 초기 연결이 만들어진 후에는 이 값이 무시됩니다. [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) 도 사용할 방법을 함께에서이 메서드로 또는 예외가 throw 됩니다.  
  
 드라이버에서는 장애 조치(Failover) 서버의 이름이 설정된 경우 장애 조치(Failover) 서버의 포트 번호를 지정할 수 없습니다. 그러나 호출는 [setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) 메서드 및 [setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) 메서드는 [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 메서드는 지원 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
