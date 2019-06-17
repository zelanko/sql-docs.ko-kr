---
title: SQLServerConnection 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a14627f54e1d297642cb2c555fb8427acb2da5a7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803084"
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 JDBC 연결을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **Implements:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerConnection은 JDBC 연결 풀링을 지원하며 물리적 JDBC 연결 또는 논리적 JDBC 연결이 될 수 있습니다. SQLServerConnection은 만들어진 모든 문에 대한 트랜잭션 컨트롤을 관리하며 XAResource 어댑터를 통해 관리되는 XA 분산 트랜잭션에 참여할 수 있습니다.  
  
 SQLServerConnection 준비 된 문 핸들의 풀을 관리 합니다. 준비된 문은 한 번만 준비하면 매개 변수의 데이터 값을 달리 하여 여러 번 실행할 수 있는 문입니다. 준비된 문은 논리적(풀링된) 연결 닫기를 통해서도 유지 관리됩니다.  
  
> [!NOTE]  
>  SQLServerConnection 스레드로부터 안전 하지 않습니다. 그러나 단일 연결에서 만들어진 여러 문을 현재 스레드에서 동시에 처리할 수 있습니다.  
  
 이 클래스는 SQLServerConnection 클래스, java.sql.connection 인터페이스 및 ISQLServerConnection 인터페이스에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
