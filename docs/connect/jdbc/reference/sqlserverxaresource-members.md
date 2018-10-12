---
title: SQLServerXAResource 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9d55da45733e15a9b2aa98f7c6d8fa386b1e4e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682691"
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|속성|설명|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|XID(XA 분기 트랜잭션 ID)가 다르지만 GTRID(전역 트랜잭션 ID)는 동일한 밀접하게 결합된 XA 트랜잭션을 허용하는 데 사용됩니다.|  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|지정된 Xid 개체가 지정하는 글로벌 트랜잭션을 커밋합니다.|  
|[end](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|트랜잭션 분기를 대신하여 수행되는 작업을 종료합니다.|  
|[forget](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|발견적으로 완료된 트랜잭션 분기에 대해 잊도록 리소스 관리자에게 지시합니다.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|이 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체에 대해 설정된 현재 트랜잭션 시간 제한 값을 가져옵니다.|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|대상 개체가 나타내는 리소스 관리자 인스턴스가 지정된 XAResource 개체에서 나타내는 리소스 관리자 인스턴스와 동일한지 확인합니다.|  
|[prepare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|지정된 Xid 개체가 지정하는 트랜잭션의 트랜잭션 커밋을 준비하도록 리소스 관리자에 요청합니다.|  
|[복구](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|리소스 관리자에서 준비된 트랜잭션 분기 목록을 가져옵니다.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|리소스 관리자에 트랜잭션 분기 대신 수행된 작업을 롤백하도록 요청합니다.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|이 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체에 대한 현재 트랜잭션 시간 제한 값을 설정합니다.|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Xid 개체에 지정된 트랜잭션 분기를 대신하여 작업을 시작합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
