---
title: "getStatementPoolingCacheSize 메서드 (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
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
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e76eb3dc67db1b3e287147ebdc2f42f719aa58fe
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>getStatementPoolingCacheSize 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 이 연결에 대 한 준비 된 문 캐시의 크기를 반환 합니다. '0' 캐싱을 사용 하도록 설정 하지 것을 의미 합니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>반환 값
 **int** 의 값이 포함 된 **statementPoolingCacheSize** 연결 속성입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
