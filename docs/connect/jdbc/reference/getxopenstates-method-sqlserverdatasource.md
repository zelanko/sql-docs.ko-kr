---
title: "getXopenStates 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 218dd99d0da0f560ae08b2bfc3edf27d3a24a960
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getxopenstates-method-sqlserverdatasource"></a>getXopenStates 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  반환 된 **부울** SQL 상태를 XOPEN 규격 상태로 변환할을 사용할 수 있는지를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** SQL 상태를 XOPEN 규격 상태로 변환할 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 XopenStates 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] SQL 상태를 XOPEN 규격 상태로 변환 합니다. 기본값은 **false**, JDBC 드라이버가 SQL 99 상태 코드를 생성 하에 이르게 됩니다. XopenStates 설정 되어 있지 않으면 getXopenStates 메서드는 기본값인을 반환 하는 **false**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

