---
title: isClosed 메서드 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6081aa34-fc88-4dd0-9a3f-05e8488219dc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a91de3a0a4e6a164f3fe290aa82148fc20239143
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isclosed-method-sqlserverresultset"></a>isClosed 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  나타냅니다 여부이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체가 잠겨 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체가 닫혀 **false** 계속 열려 있으면입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isClosed 메서드는 java.sql.ResultSet 인터페이스의 isClosed 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
