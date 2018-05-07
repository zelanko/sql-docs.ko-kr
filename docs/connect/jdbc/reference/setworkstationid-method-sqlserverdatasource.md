---
title: setWorkstationID 메서드 (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae8a5eeefcad88ae35c2ce4388d09b555a495a30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
 클라이언트 컴퓨터 이름이 포함된 **문자열**입니다.  
  
## <a name="remarks"></a>주의  
 workstationID는 클라이언트 컴퓨터 또는 워크스테이션의 이름입니다. WorkstationID 속성이 설정 하지 않으면 기본값 InetAddress.getLocalHost().getHostName() 메서드를 호출 하 여 생성 됩니다. GetHostName 빈 값을 반환할 경우 getHostAddress().toString() 메서드 호출 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
