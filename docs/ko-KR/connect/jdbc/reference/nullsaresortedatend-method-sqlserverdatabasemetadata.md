---
title: nullsAreSortedAtEnd 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.nullsAreSortedAtEnd
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 713cf636-40f2-474a-8a5d-5aba4a310a9c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 666aa334bc08bd231cab37f7e6d1b88d82a42556
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="nullsaresortedatend-method-sqlserverdatabasemetadata"></a>nullsAreSortedAtEnd 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  정렬 순서에 관계없이 NULL 값이 끝에 정렬되는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean nullsAreSortedAtEnd()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 끝에 정렬 하는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 nullsAreSortedAtEnd 메서드는 java.sql.DatabaseMetaData 인터페이스의 nullsAreSortedAtEnd 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
