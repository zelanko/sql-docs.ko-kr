---
title: setUser 메서드 (SQLServerDataSource) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b8b93bf8205bcf1cf828ab53c7a2842e13a9f4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="setuser-method-sqlserverdatasource"></a>setUser 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 사용자 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *user*  
  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 SetUser 메서드를 연결 하는 데 사용할 사용자 이름을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 사용자 이름 값을 설정 하지는 [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) 메서드 기본값인 null 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
