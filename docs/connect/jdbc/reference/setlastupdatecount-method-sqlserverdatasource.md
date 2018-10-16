---
title: setLastUpdateCount 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3369fbc84cb16ed0f9b587ed20fe7fe368d11b02
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49084917"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  lastUpdateCount 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *lastUpdateCount*  
  
 lastUpdateCount가 사용되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>Remarks  
 lastUpdateCount 속성이 **true**로 설정된 경우 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 SQL 문에서 서버로 전달된 마지막 업데이트 횟수만 반환합니다. lastUpdateCount 속성이 **false**로 설정된 경우 드라이버에서는 실행된 모든 트리거에서 반환된 업데이트 횟수를 포함하여 모든 업데이트 횟수를 반환합니다. lastUpdateCount 속성이 설정되어 있지 않으면 [getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) 메서드는 기본값인 **true**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
