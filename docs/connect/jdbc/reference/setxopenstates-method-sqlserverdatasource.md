---
title: "setXopenStates 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 857d9f914e10365746381ee4335f35f19d4beedd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** SQL 상태를 XOPEN 규격 상태로 변환할을 사용할 수 있는지를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *xopenStates*  
  
 **true 이면** SQL 상태를 XOPEN 규격 상태로 변환할 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 XopenStates 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] SQL 상태를 XOPEN 규격 상태로 변환 합니다. 기본값은 **false**, JDBC 드라이버가 SQL 99 상태 코드를 생성 하에 이르게 됩니다. XopenStates 설정 되어 있지 않으면는 [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) 메서드는 기본값인을 반환 **false**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

