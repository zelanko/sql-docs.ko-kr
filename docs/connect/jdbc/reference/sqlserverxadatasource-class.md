---
description: SQLServerXADataSource 클래스
title: SQLServerXADataSource 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 775768de5cd833a6fdc9d496c5d94653bcf4ef09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462605"
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
  
## <a name="remarks"></a>설명  
 SQLServerXADataSource 인터페이스를 구현하는 개체는 일반적으로 JNDI(Java Naming and Directory Interface)를 사용하는 명명 서비스에 등록됩니다.  
  
 SQLServerXADataSource 클래스에서는 분산(XA) 트랜잭션에서 사용할 데이터베이스 연결을 제공합니다. SQLServerXADataSource 클래스에서는 물리적 연결의 연결 풀링도 지원합니다. javax.sql 패키지에 정의된 SQLServerXADataSource 및 SQLServerXAConnection 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 구현됩니다.  
  
 SQLServerXAConnection 개체는 분산 트랜잭션에 참여할 수 있는 풀링된 연결입니다. 더 정확하게 말하자면 SQLServerXAConnection은 [getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md) 메서드를 추가하여 SQLServerPooledConnection 인터페이스를 확장합니다. 이 메서드는 트랜잭션 관리자가 이 연결에서 수행되는 작업을 분산 트랜잭션의 다른 참가자와 함께 조정하는 데 사용할 수 있는 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체를 생성합니다. SQLServerPooledConnection 인터페이스를 확장하므로 SQLServerXAConnection 개체는 SQLServerPooledConnection 개체의 모든 메서드를 지원합니다. 이러한 개체는 기본 데이터 원본에 대한 재사용 가능한 실제 연결이며, JDBC 애플리케이션에 다시 전달할 수 있는 논리적 연결 핸들을 생성합니다.  
  
 SQLServerXAConnection 개체는 SQLServerXADataSource 개체에 의해 생성됩니다. SQLServerConnectionPoolDataSource 개체 및 SQLServerXADataSource 개체는 둘 다 JDBC 애플리케이션에서 볼 수 있는 데이터 원본 계층 아래에 구현되므로 서로 비슷합니다. 이 아키텍처를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 애플리케이션에 투명한 방식으로 분산 트랜잭션을 지원합니다. SQLServerXADataSource는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] DTC(Distributed Transaction Coordinator)와 통합되어 진정한 분산 트랜잭션 처리를 제공하도록 구성할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXADataSource 멤버](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
