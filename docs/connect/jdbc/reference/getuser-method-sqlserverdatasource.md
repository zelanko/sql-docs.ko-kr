---
title: "getUser 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9de58a65490961002fbdcfa37d0a2367ca078382
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getuser-method-sqlserverdatasource"></a>getUser 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 메서드의 인스턴스에 연결할 때 사용할 사용자 이름을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 사용자 이름 값이 설정되어 있지 않으면 getUser 메서드는 기본값인 null을 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

