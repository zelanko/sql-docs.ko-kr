---
title: SQLServerXAResource 멤버 | Microsoft Docs
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
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 042e159030fde83ce41eb9aef8804f02c9d2ee8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에서 노출 하는 멤버는 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|이름|Description|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|XID(XA 분기 트랜잭션 ID)가 다르지만 GTRID(전역 트랜잭션 ID)는 동일한 밀접하게 결합된 XA 트랜잭션을 허용하는 데 사용됩니다.|  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|지정된 된 Xid 개체에서 지정 된 전역 트랜잭션을 커밋합니다.|  
|[끝](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|트랜잭션 분기를 대신하여 수행되는 작업을 종료합니다.|  
|[제거](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|발견적으로 완료된 트랜잭션 분기에 대해 잊도록 리소스 관리자에게 지시합니다.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|이 대 한 설정 현재 트랜잭션 시간 제한 값을 가져옵니다. [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체입니다.|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|대상 개체가 나타내는 리소스 관리자 인스턴스가 지정 된 XAResource 개체가 나타내는 리소스 관리자 인스턴스와 동일 인지 여부를 확인 합니다.|  
|[준비](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|지정된 된 Xid 개체에서 지정 된 트랜잭션의 트랜잭션 커밋을 준비 하도록 리소스 관리자 요청 수입니다.|  
|[복구](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|리소스 관리자에서 준비된 트랜잭션 분기 목록을 가져옵니다.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|리소스 관리자에 트랜잭션 분기 대신 수행된 작업을 롤백하도록 요청합니다.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|이 대 한 현재 트랜잭션 시간 제한 값을 설정 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체입니다.|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Xid 개체에 지정 된 트랜잭션 분기를 대신 하 여 작업을 시작 합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
