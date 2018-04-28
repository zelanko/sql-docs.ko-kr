---
title: recover 메서드 (SQLServerXAResource) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ae101421d8ea82742a631b9f8908aa075a99920
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="recover-method-sqlserverxaresource"></a>recover 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  리소스 관리자에서 준비된 트랜잭션 분기 목록을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *flags*  
  
 **int** 다음 값 중 하나를 수행 하는 값: XAResource.TMSTARTRSCAN 또는 XAResource.TMENDRSCAN 또는 XAResource.TMNOFLAGS XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN 합니다.  
  
## <a name="return-value"></a>반환 값  
 Xid 개체입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>주의  
 이 복구 메서드는 javax.transaction.xa.XAResource 인터페이스의 복구 메서드에 의해 지정 됩니다.  
  
 경우 매개 변수 **플래그** XAResource.TMSTARTRSCAN 또는 XAResource.TMSTARTRSCAN 아닙니다 | XAResource.TMENDRSCAN, 복구 검색이 진행 중 이어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
