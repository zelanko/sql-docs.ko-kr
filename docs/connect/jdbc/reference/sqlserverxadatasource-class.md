---
title: SQLServerXADataSource 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa85b61a67655fbf363c1927b48cd79f8ff841ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774421"
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  내부적으로 사용되는 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체에 대한 팩터리를 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **구현:** javax.sql.XADataSource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerXADataSource 인터페이스를 구현하는 개체는 일반적으로 JNDI(Java Naming and Directory Interface)를 사용하는 명명 서비스에 등록됩니다.  
  
 SQLServerXADataSource 클래스에서는 분산(XA) 트랜잭션에서 사용할 데이터베이스 연결을 제공합니다. SQLServerXADataSource 클래스는 또한 실제 연결의 연결 풀링도 지원 합니다. Javax.sql 패키지에에서 정의 되는 SQLServerXAConnection 및 SQLServerXADataSource 인터페이스를 구현한는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 SQLServerXAConnection 개체는 분산 트랜잭션에 참여할 수 있는 풀링된 연결입니다. SQLServerXAConnection 메서드를 추가 하 여 SQLServerPooledConnection 인터페이스를 확장 하는 보다 정확 하 게 [getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)합니다. 이 메서드는 트랜잭션 관리자가 이 연결에서 수행되는 작업을 분산 트랜잭션의 다른 참가자와 함께 조정하는 데 사용할 수 있는 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체를 생성합니다. SQLServerPooledConnection 인터페이스를 확장 하므로 해당 SQLServerXAConnection 개체 SQLServerPooledConnection 개체의 모든 메서드를 지원 합니다. 이러한 개체는 기본 데이터 원본에 대한 재사용 가능한 실제 연결이며, JDBC 응용 프로그램에 다시 전달할 수 있는 논리적 연결 핸들을 생성합니다.  
  
 SQLServerXAConnection 개체 SQLServerXADataSource 개체에 의해 생성 됩니다. SQLServerConnectionPoolDataSource 개체 및 SQLServerXADataSource 개체는는 둘 다 JDBC 응용 프로그램에 표시 되는 데이터 원본 계층 아래 구현 되므로 서로 비슷합니다. 이 아키텍처를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 응용 프로그램에 투명한 방식으로 분산 트랜잭션을 지원합니다. SQLServerXADataSource는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] DTC(Distributed Transaction Coordinator)와 통합되어 진정한 분산 트랜잭션 처리를 제공하도록 구성할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXADataSource 멤버](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
