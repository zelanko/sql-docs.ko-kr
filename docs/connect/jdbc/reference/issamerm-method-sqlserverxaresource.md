---
title: "isSameRM 메서드 (SQLServerXAResource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27cc769b71dffcb47c1575c73c778fbd43e73656
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="issamerm-method-sqlserverxaresource"></a>isSameRM 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  대상 개체가 나타내는 리소스 관리자 인스턴스가 지정 된 XAResource 개체가 나타내는 리소스 관리자 인스턴스와 같은 인지 여부를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *xares*  
  
 XAResource 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 인스턴스는 동일 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>주의  
 이 커밋 메서드는 javax.transaction.xa.XAResource 인터페이스의 커밋 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
