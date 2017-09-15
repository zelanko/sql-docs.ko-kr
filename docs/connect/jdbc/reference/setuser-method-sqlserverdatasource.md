---
title: "setUser 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bdb6e334866ae6561fc770c36dfcfa4c0f0a4898
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setuser-method-sqlserverdatasource"></a>setUser 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 사용자 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용자*  
  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 SetUser 메서드를 연결 하는 데 사용할 사용자 이름을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 사용자 이름 값을 설정 하지는 [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) 메서드 기본값인 null 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
