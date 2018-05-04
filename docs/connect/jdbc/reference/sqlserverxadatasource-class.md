---
title: SQLServerXADataSource 클래스 | Microsoft Docs
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
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb52f851b776b14c99ba98d64fabfc964b8029cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  에 대 한 팩터리를 나타내는 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 내부적으로 사용 되는 개체입니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **구현:** javax.sql.XADataSource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>주의  
 SQLServerXADataSource 인터페이스를 구현 하는 개체는 일반적으로 Java Naming and Directory 인터페이스 JNDI ()를 사용 하는 명명 서비스에 등록 됩니다.  
  
 SQLServerXADataSource 클래스에서는 분산된 (XA) 트랜잭션에서 사용할 데이터베이스 연결을 제공합니다. SQLServerXADataSource 클래스는 또한 실제 연결의 연결 풀링도 지원 합니다. Javax.sql 패키지에에서 정의 된 SQLServerXADataSource 및 SQLServerXAConnection 인터페이스 구현 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
 SQLServerXAConnection 개체에는 분산 트랜잭션에 참여할 수 있는 풀링된 연결입니다. SQLServerXAConnection 메서드를 추가 하 여 SQLServerPooledConnection 인터페이스를 확장 하는 보다 정확 하 게 [getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)합니다. 이 메서드는 생성 된 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 분산 트랜잭션의 다른 참가자와 함께이 연결에서 수행 하는 작업을 조정 하는 트랜잭션 관리자가 사용할 수 있는 개체입니다. SQLServerPooledConnection 인터페이스를 확장 하므로 SQLServerXAConnection 개체 SQLServerPooledConnection 개체의 모든 메서드를 지원 합니다. 이러한 개체는 기본 데이터 원본에 대한 재사용 가능한 실제 연결이며, JDBC 응용 프로그램에 다시 전달할 수 있는 논리적 연결 핸들을 생성합니다.  
  
 SQLServerXAConnection 개체 SQLServerXADataSource 개체에 의해 생성 됩니다. 개체 SQLServerConnectionPoolDataSource 및 SQLServerXADataSource 개체 되므로 서로 비슷합니다는 둘 다 JDBC 응용 프로그램에서 표시 되는 데이터 원본 계층 아래 구현 합니다. 이 아키텍처를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 응용 프로그램에 투명 한 방식으로 분산된 트랜잭션을 지원 합니다. SQLServerXADataSource와 통합 하도록 구성할 수 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Coordinator DTC (Distributed Transaction) true 수 있도록 분산 트랜잭션 처리 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXADataSource 멤버](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
