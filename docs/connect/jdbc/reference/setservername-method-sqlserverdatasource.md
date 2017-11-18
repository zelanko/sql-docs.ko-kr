---
title: "setServerName 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2efdbb68c0d546776b7027c9130e7589c92322ea
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  실행 중인 컴퓨터의 이름을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *서버 이름*  
  
 A **문자열** 서버 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 서버 이름은 실행 하는 대상 컴퓨터의 호스트 이름을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. ServerName 속성을 설정 하지 않으면 경우 [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) 기본값인 null 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

