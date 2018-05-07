---
title: SQLServerConnection 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f59867c195a333d0bd4bee7996d19fbeae156c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 연결을 나타내며는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>주의  
 SQLServerConnection은 JDBC 연결 풀링을 지원 하며 물리적 JDBC 연결 이거나 논리적 JDBC 연결 일 수 있습니다. SQLServerConnection,에서 만들어진 모든 문에 대 한 트랜잭션 제어를 관리 하 고 XAResource 어댑터를 통해 관리 되는 XA 분산 트랜잭션에 참여할 수 있습니다.  
  
 SQLServerConnection 준비 된 문 핸들의 풀을 관리합니다. 준비된 문은 한 번만 준비하면 매개 변수의 데이터 값을 달리 하여 여러 번 실행할 수 있는 문입니다. 준비된 문은 논리적(풀링된) 연결 닫기를 통해서도 유지 관리됩니다.  
  
> [!NOTE]  
>  SQLServerConnection 스레드로부터 안전 하지 않습니다. 그러나 단일 연결에서 만들어진 여러 문을 현재 스레드에서 동시에 처리할 수 있습니다.  
  
 이 클래스는 SQLServerConnection 클래스, java.sql.connection 인터페이스 및 ISQLServerConnection 인터페이스에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
