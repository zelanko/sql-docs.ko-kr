---
title: "setLastUpdateCount 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: caa3caa684088a38b732dddae8b17b7c88cf76bb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** lastUpdateCount 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *lastUpdateCount*  
  
 **true 이면** lastUpdateCount가 사용 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 LastUpdateCount 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 마지막만를 반환 합니다는 SQL 문 업데이트 횟수 서버에 전달 합니다. LastUpdateCount 속성이로 설정 되어 있으면 **false**, 드라이버 업데이트 모든 업데이트 발생 가능성이 있는 모든 트리거에서 반환 하는 것을 포함 하는 횟수를 반환 합니다. LastUpdateCount 속성이 설정 하지 않으면는 [getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) 메서드는 기본값인을 반환 **true**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

