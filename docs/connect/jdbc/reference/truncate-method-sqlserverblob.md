---
title: "truncate 메서드 (SQLServerBlob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerBlob.truncate
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3931e5adc705ed7f111eaf8d41f08c52ba66944
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="truncate-method-sqlserverblob"></a>truncate 메서드(SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB을 지정된 길이로 자릅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *len 함수*  
  
 BLOB의 새 길이입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 자르기 메서드는 java.sql.Blob 인터페이스의 자르기 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
