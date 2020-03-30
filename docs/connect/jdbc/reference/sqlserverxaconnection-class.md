---
title: SQLServerXAConnection 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32d538e31ca3f4a0d9b23411ebcb7b282df46b33
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970314"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  분산(XA) 트랜잭션에 참여할 수 있는 JDBC 연결을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **구현:** javax.sql.XAConnection  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>설명  
 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체를 사용하여 SQLServerXAConnection 개체를 분산 트랜잭션에 참여시킬 수 있습니다. 일반적으로 중간 계층 서버에 속한 트랜잭션 관리자는 SQLServerXAResource 개체를 통해 SQLServerXAConnection 개체를 관리합니다.  
  
> [!NOTE]  
>  애플리케이션 프로그래머는 일반적으로 이 인터페이스를 직접 사용하지 않습니다. 이 인터페이스는 중간 계층 서버에서 작업하는 트랜잭션 관리자가 주로 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
