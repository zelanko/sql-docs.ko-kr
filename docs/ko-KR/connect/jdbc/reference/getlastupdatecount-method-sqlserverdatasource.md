---
title: getLastUpdateCount 메서드 (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4688052547e9bf38cf8184fc67d14a3253edcb8d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  반환 된 **부울** lastUpdateCount 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** lastUpdateCount가 사용 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 LastUpdateCount 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 마지막만를 반환 합니다 업데이트 횟수 SQL 문에서 서버로 전달 합니다. LastUpdateCount 속성이로 설정 되어 있으면 **false**, 드라이버 업데이트 모든 업데이트 발생 가능성이 있는 모든 트리거에서 반환 하는 것을 포함 하는 횟수를 반환 합니다. LastUpdateCount 속성이 사용을 설정 하지 않으면 getLastUpdateCount 메서드는의 기본 값을 반환 **true**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
