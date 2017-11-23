---
title: "setWorkstationID 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.setWorkstationID
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd2d1ad16dd1ff622c7d8f4f8394df08bdfd3f6a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터의 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *workstationID*  
  
 A **문자열** 클라이언트 컴퓨터 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 workstationID는 클라이언트 컴퓨터 또는 워크스테이션의 이름입니다. WorkstationID 속성이 설정 하지 않으면 기본값 InetAddress.getLocalHost().getHostName() 메서드를 호출 하 여 생성 됩니다. GetHostName 빈 값을 반환할 경우 getHostAddress().toString() 메서드 호출 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
