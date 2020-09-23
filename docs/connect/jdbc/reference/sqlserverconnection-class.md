---
title: SQLServerConnection 클래스
description: SQL Server용 JDBC Driver의 SQLServerConnection 클래스에 대한 공용 API를 자세히 알아봅니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6827b79b4d1cc7b3f66db3c53c338614ec49fc3
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411479"
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
  
## <a name="remarks"></a>설명  
 SQLServerConnection은 JDBC 연결 풀링을 지원하며 물리적 JDBC 연결 또는 논리적 JDBC 연결이 될 수 있습니다. SQLServerConnection은 만들어진 모든 문에 대한 트랜잭션 컨트롤을 관리하며 XAResource 어댑터를 통해 관리되는 XA 분산 트랜잭션에 참여할 수 있습니다.  
  
 SQLServerConnection은 준비된 문 핸들의 풀을 관리합니다. 준비된 문은 한 번만 준비하면 매개 변수의 데이터 값을 달리 하여 여러 번 실행할 수 있는 문입니다. 준비된 문은 논리적(풀링된) 연결 닫기를 통해서도 유지 관리됩니다.  
  
> [!NOTE]  
>  SQLServerConnection은 스레드로부터 안전하지 않습니다. 그러나 단일 연결에서 만들어진 여러 문을 현재 스레드에서 동시에 처리할 수 있습니다.  
  
 이 클래스는 SQLServerConnection 클래스, java.sql.connection 인터페이스 및 ISQLServerConnection 인터페이스에 대한 래핑 해제를 지원합니다. 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
