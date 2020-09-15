---
description: truncate 메서드(SQLServerClob)
title: truncate 메서드(SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d25deb243f43b3c4ae4cd82d561e581cc5b5ba95
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431425"
---
# <a name="truncate-method-sqlserverclob"></a>truncate 메서드(SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  CLOB을 지정된 길이로 자릅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *len*  
  
 CLOB을 자른 결과 값의 길이(문자 수)입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>설명  
 이 truncate 메서드는 java.sql.Clob 인터페이스의 truncate 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
