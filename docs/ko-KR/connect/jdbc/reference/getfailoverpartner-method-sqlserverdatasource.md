---
title: getFailoverPartner 메서드 (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6330d85cd9625854049ef5ec51bedff223a23198
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>getFailoverPartner 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 설정 하지 않은 경우 장애 조치 파트너 또는 null의 이름을 포함 하 합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드에 의해 반환 되는 값의 장애 조치 파트너 이름을 사용 하 여 집합에 반영 된 [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
