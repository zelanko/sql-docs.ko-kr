---
description: 트랜잭션 잠금 및 행 버전 관리 지침
title: 트랜잭션 잠금 및 행 버전 관리 지침
ms.custom: seo-dt-2019
ms.date: 03/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- guide, transaction locking and row versioning
- transaction locking and row versioning guide
- lock compatibility matrix, [SQL Server]
- lock granularity and hierarchies, [SQL Server]
- deadlocks, [SQL Server]
- lock escalation, [SQL Server]
- lock partitioning, [SQL Server]
ms.assetid: 44fadbee-b5fe-40c0-af8a-11a1eecf6cb7
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 815ad066f97a80d250dcd1c3b1a961e4a86b05a6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416857"
---
# <a name="transaction-locking-and-row-versioning-guide"></a>트랜잭션 잠금 및 행 버전 관리 지침
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

어느 데이터베이스에서든 트랜잭션을 제대로 관리하지 않으면 사용자가 많은 시스템에 경합 및 성능 문제가 발생할 수 있습니다. 데이터에 액세스하는 사용자 수가 늘어나면 애플리케이션에서 트랜잭션을 효율적으로 사용하는 것이 중요합니다. 이 지침에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 각 트랜잭션의 물리적 무결성을 유지하는 데 사용하는 잠금 및 행 버전 관리 메커니즘과 애플리케이션에서 트랜잭션을 효율적으로 제어할 수 있는 방법에 대해 설명합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](별도로 언급하지 않는 한 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]~[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 
  
##  <a name="transaction-basics"></a><a name="Basics"></a> 트랜잭션 기본 사항  
 트랜잭션은 하나의 논리적 작업 단위로 수행되는 일련의 작업입니다. 작업의 논리적 단위는 ACID(원자성, 일관성, 격리성 및 영속성) 속성이라고 하는 네 가지 속성을 통해 트랜잭션으로서의 자격을 부여합니다.  
  
 **원자성**  
 트랜잭션은 더 이상 분류할 수 없는 작업 단위여야 하며 모든 데이터 수정 작업이 수행되거나 하나도 수행되지 말아야 합니다.  
  
 **일관성**  
 완료된 트랜잭션의 모든 데이터는 일관되어야 합니다. 관계형 데이터베이스에서는 트랜잭션 수정에 모든 규칙을 적용하여 모든 데이터 무결성을 유지해야 합니다. 트랜잭션 마지막에는 B-tree 인덱스 또는 이중 연결 목록 등 모든 내부적 데이터 구조를 반드시 수정해야 합니다.  
  
 **격리**  
 동시 트랜잭션에 의한 수정은 다른 동시 트랜잭션에 의한 수정과 격리되어야 합니다. 트랜잭션에서 다른 동시 트랜잭션이 수정하기 전 상태의 데이터를 보거나 두 번째 트랜잭션이 완료된 후의 데이터를 볼 수는 있지만 중간 상태는 볼 수 없습니다. 결과적으로 시작 데이터를 다시 로드하고 일련의 트랜잭션을 재생하여 원래 트랜잭션이 수행된 후의 상태로 데이터를 되돌릴 수 있는데 이를 순차성이라고 합니다.  
  
 **영속성**  
 완전 내구성이 있는 트랜잭션이 완료되고 나면 그 영향이 영구적으로 시스템에 적용됩니다. 수정은 시스템에 오류가 발생한 경우에도 지속됩니다. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 이상에서 지연된 영구 트랜잭션을 사용할 수 있습니다. 지연된 영구적 트랜잭션은 트랜잭션 로그 레코드가 디스크에 유지되기 전에 커밋됩니다. 지연된 트랜잭션 내구성에 대한 자세한 내용은 [트랜잭션 내구성](../relational-databases/logs/control-transaction-durability.md) 항목을 참조하세요.  
  
 SQL 프로그래머는 적시에 트랜잭션을 시작하고 끝내 데이터의 논리적 일관성을 유지하는 책임을 맡고 있습니다. 프로그래머는 조직의 업무 규칙과 관련하여 데이터를 일관된 상태로 유지할 수 있도록 데이터 수정 순서를 정의해야 합니다. 그런 다음 이러한 수정 문을 하나의 트랜잭션에 포함하여 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]가 트랜잭션의 물리적 무결성을 유지할 수 있게 해야 합니다.  
  
 각 트랜잭션의 물리적 무결성을 유지하는 메커니즘을 제공하는 것은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]과 같은 기업 데이터베이스 시스템의 책임입니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 다음을 제공합니다.  
  
-   트랜잭션 격리성을 유지하는 잠금 기능  
  
-   로깅 기능은 트랜잭션 내구성을 유지합니다. 완전 내구성 있는 트랜잭션의 경우 트랜잭션이 커밋되기 전에 로그 레코드가 디스크에 확정됩니다. 따라서 서버 하드웨어, 운영 체제 또는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 인스턴스 자체에 오류가 발생하더라도, 인스턴스는 다시 시작될 때 트랜잭션 로그를 사용하여 불완전한 트랜잭션을 자동으로 시스템 오류 시점으로 롤백합니다. 지연된 영구적 트랜잭션은 트랜잭션 로그 레코드가 디스크에 유지되기 전에 커밋됩니다. 이러한 트랜잭션은 로그 레코드가 디스크에 확정되기 전에 시스템 오류가 발생하면 손실될 수 있습니다. 지연된 트랜잭션 내구성에 대한 자세한 내용은 [트랜잭션 내구성](../relational-databases/logs/control-transaction-durability.md) 항목을 참조하세요.  
  
-   트랜잭션 원자성 및 일관성을 유지하는 트랜잭션 관리 기능. 트랜잭션이 일단 시작된 후에는 성공적으로 완료(커밋)되어야 합니다. 그렇지 않으면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]이 트랜잭션 시작 이후 만들어진 모든 데이터 수정 내용을 실행 취소합니다. 이 작업은 변경 전의 상태를 데이터에 반환하기 때문에 트랜잭션 롤백이라고도 합니다.  
  
### <a name="controlling-transactions"></a>트랜잭션 제어  
 애플리케이션은 주로 트랜잭션 시작 및 종료 시기를 지정하여 트랜잭션을 제어합니다. 트랜잭션 시작 및 종료 시기는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 또는 데이터베이스 API(응용 프로그래밍 인터페이스) 함수를 사용하여 지정할 수 있습니다. 시스템은 트랜잭션을 불완전하게 종료하는 오류를 올바르게 처리할 수도 있어야 합니다. 자세한 내용은 [트랜잭션](../t-sql/language-elements/transactions-transact-sql.md), [ODBC의 트랜잭션](../relational-databases/native-client/odbc/performing-transactions-in-odbc.md) 및 [OLEDB(SQL Server Native Client)의 트랜잭션](../relational-databases/native-client-ole-db-transactions/transactions.md)을 참조하세요.  
  
 기본적으로 트랜잭션은 연결 수준에서 관리됩니다. 한 연결에서 트랜잭션이 시작되면 트랜잭션이 끝날 때까지 해당 연결에서 실행되는 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 트랜잭션의 일부가 됩니다. 그러나 MARS(Multiple Active Result Set) 세션에서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 명시적 또는 암시적 트랜잭션이 일괄 처리 수준에서 관리되는 일괄 처리 범위의 트랜잭션이 됩니다. 일괄 처리가 완료될 때 일괄 처리 범위의 트랜잭션이 커밋되거나 롤백되지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 해당 트랜잭션을 자동으로 롤백합니다. 자세한 내용은 [MARS(Multiple Active Result Sets) 사용](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.  
  
#### <a name="starting-transactions"></a>트랜잭션 시작  
 API 함수와 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용하여 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에서 명시적, 자동 커밋 또는 암시적 트랜잭션을 시작할 수 있습니다.  
  
 **명시적 트랜잭션**  
 명시적 트랜잭션은 API 함수를 통해 또는 [!INCLUDE[tsql](../includes/tsql-md.md)] BEGIN TRANSACTION, COMMIT TRANSACTION, COMMIT WORK, ROLLBACK TRANSACTION 또는 ROLLBACK WORK [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하여 트랜잭션 시작 및 완료를 모두 명시적으로 정의하는 트랜잭션입니다. 트랜잭션이 끝나면 명시적 트랜잭션이 시작된 시기의 트랜잭션 모드인 암시적 모드나 자동 커밋 모드로 되돌려집니다.  
  
 명시적 트랜잭션에서는 다음 문을 제외한 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
:::row:::
    :::column:::
        ALTER DATABASE
    :::column-end:::
    :::column:::
        CREATE DATABASE
    :::column-end:::
    :::column:::
        DROP FULLTEXT INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER FULLTEXT CATALOG
    :::column-end:::
    :::column:::
        CREATE FULLTEXT CATALOG
    :::column-end:::
    :::column:::
        RECONFIGURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER FULLTEXT INDEX
    :::column-end:::
    :::column:::
        CREATE FULLTEXT INDEX
    :::column-end:::
    :::column:::
        RESTORE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BACKUP
    :::column-end:::
    :::column:::
        DROP DATABASE
    :::column-end:::
    :::column:::
        전체 텍스트 시스템 저장 프로시저
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE DATABASE
    :::column-end:::
    :::column:::
        DROP FULLTEXT CATALOG
    :::column-end:::
    :::column:::
        데이터베이스 옵션을 설정하는 sp_dboption 또는 명시적/암시적 트랜잭션 내에서 master 데이터베이스를 수정하는 시스템 프로시저
    :::column-end:::
:::row-end:::

> [!NOTE]  
> UPDATE STATISTICS는 명시적 트랜잭션 내에서 사용할 수 있습니다. 그러나 UPDATE STATISTICS는 포함하는 트랜잭션과 별개로 커밋하며 롤백할 수 없습니다.  
  
 **자동 커밋 트랜잭션**  
 자동 커밋 모드는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 기본 트랜잭션 관리 모드입니다. 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 완료 시 커밋되거나 롤백됩니다. 문이 성공적으로 완료되면 커밋되며 오류가 발생하면 롤백됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스 연결은 명시적 트랜잭션이나 암시적 트랜잭션에 의해 이 기본 모드가 무시되지 않는 한 자동 커밋 모드로 작동합니다. 자동 커밋 모드는 또한 ADO, OLE DB, ODBC 및 DB-Library의 기본 모드이기도 합니다.  
  
 **암시적 트랜잭션**  
 연결이 암시적 트랜잭션 모드에서 작동할 때는 현재 트랜잭션이 커밋 또는 롤백된 후 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에서 자동으로 새 트랜잭션을 시작합니다. 트랜잭션 시작을 직접 지정할 필요 없이 각 트랜잭션을 커밋 또는 롤백하기만 하면 됩니다. 암시적 트랜잭션 모드는 트랜잭션의 연속 체인을 생성합니다. API 함수나 [!INCLUDE[tsql](../includes/tsql-md.md)] SET IMPLICIT_TRANSACTIONS ON 문을 통해 암시적 트랜잭션 모드를 설정합니다.  이 모드를 자동 커밋 OFF라고 하며 [JDBC의 setAutoCommit 메서드](../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)를 참조하세요. 
  
 연결에 대해 암시적 트랜잭션 모드를 설정하고 나면 이러한 문을 처음 실행할 때 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스가 자동으로 트랜잭션을 시작합니다.  
  
:::row:::
    :::column:::
        ALTER TABLE
    :::column-end:::
    :::column:::
        FETCH
    :::column-end:::
    :::column:::
        REVOKE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE
    :::column-end:::
    :::column:::
        GRANT
    :::column-end:::
    :::column:::
        SELECT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        Delete
    :::column-end:::
    :::column:::
        INSERT
    :::column-end:::
    :::column:::
        TRUNCATE TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DROP
    :::column-end:::
    :::column:::
        OPEN
    :::column-end:::
    :::column:::
        UPDATE
    :::column-end:::
:::row-end:::

-  **일괄 처리 범위의 트랜잭션**  
   MARS(Multiple Active Result Sets)에만 해당되며, MARS 세션에서 시작되는 [!INCLUDE[tsql](../includes/tsql-md.md)] 명시적 또는 암시적 트랜잭션이 일괄 처리 범위 트랜잭션이 됩니다. 일괄 처리가 완료될 때 커밋되거나 롤백되지 않은 일괄 처리 범위의 트랜잭션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 자동으로 롤백합니다.  
  
-  **분산 트랜잭션**  
   분산 트랜잭션은 리소스 관리자라고 하는 둘 이상의 서버에 분산됩니다. 트랜잭션 관리는 트랜잭션 관리자라고 하는 서버 구성 요소에 의해 리소스 관리자 간에 조정되어야 합니다. MS DTC([!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 [!INCLUDE[msCoName](../includes/msconame-md.md)] Distributed Transaction Coordinator) 등의 트랜잭션 관리자 또는 분산 트랜잭션 처리용 Open Group XA 사양을 지원하는 기타 트랜잭션 관리자에 의해 조정되는 분산 트랜잭션에서 리소스 관리자 역할을 합니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.  
  
   둘 이상의 데이터베이스에 분산된 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 단일 인스턴스 내에 있는 트랜잭션은 실제로 분산 트랜잭션입니다. 인스턴스는 분산 트랜잭션을 내부적으로 관리하므로 사용자에게는 로컬 트랜잭션처럼 작동합니다.  
  
   애플리케이션에서의 분산 트랜잭션 관리 방법은 로컬 트랜잭션과 많은 부분이 동일합니다. 트랜잭션이 끝나면 애플리케이션이 트랜잭션을 커밋 또는 롤백하도록 요청합니다. 트랜잭션 관리자는 분산 커밋을 다른 방법으로 관리하여 일부 리소스 관리자는 성공적으로 커밋하고 일부는 트랜잭션을 롤백하는 네트워크 오류의 발생 가능성을 최소화해야 합니다. 이렇게 하려면 커밋 프로세스를 준비 단계와 커밋 단계로 관리해야 하는데 이러한 방법을 2단계 커밋(2PC)이라고 합니다.  
  
   -  **준비 단계**  
      트랜잭션 관리자가 커밋 요청을 수신하면 트랜잭션과 관련된 모든 리소스 관리자에게 준비 명령을 보냅니다. 그런 다음 각 리소스 관리자는 트랜잭션을 지속적으로 만들고 트랜잭션에 대한 로그 이미지를 갖고 있는 버퍼를 디스크로 플러시하는 데 필요한 모든 작업을 수행합니다. 각 리소스 관리자가 준비 단계를 완료하면 준비 성공 또는 실패 여부를 트랜잭션 관리자에게 반환합니다. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서 지연된 트랜잭션 내구성이 도입되었습니다. 지연된 영구적 트랜잭션은 트랜잭션 로그 이미지가 디스크에 플러시되기 전에 커밋됩니다. 지연된 트랜잭션 내구성에 대한 자세한 내용은 [트랜잭션 내구성](../relational-databases/logs/control-transaction-durability.md) 항목을 참조하세요.  
  
   -  **커밋 단계**  
      트랜잭션 관리자가 모든 리소스 관리자로부터 준비 성공 알림을 받으면 각 리소스 관리자에게 커밋 명령을 보냅니다. 그런 다음에는 리소스 관리자가 커밋을 완료할 수 있습니다. 모든 리소스 관리자가 성공적인 커밋을 보고하면 트랜잭션 관리자가 애플리케이션에 성공을 알립니다. 준비 실패를 보고한 리소스 관리자가 있으면 트랜잭션 관리자가 각 리소스 관리자에게 롤백 명령을 보내서 애플리케이션에게 커밋 실패를 알립니다.  
  
      [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 애플리케이션은 [!INCLUDE[tsql](../includes/tsql-md.md)] 또는 데이터베이스 API를 통해 분산 트랜잭션을 관리할 수 있습니다. 자세한 내용은 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)를 참조하세요.  
  
#### <a name="ending-transactions"></a>트랜잭션 종료  
 COMMIT 또는 ROLLBACK 문을 사용하거나 해당 API 함수를 통해 트랜잭션을 종료할 수 있습니다.  
  
-  **COMMIT**  
   트랜잭션이 성공하면 커밋합니다. COMMIT 문을 사용하면 모든 트랜잭션 수정이 영구적으로 데이터베이스의 일부로 적용됩니다. COMMIT은 또한 트랜잭션에 사용된 잠금과 같은 리소스를 해제합니다.  
  
-  **ROLLBACK**  
   트랜잭션에서 오류가 발생하거나 사용자가 트랜잭션을 취소하려고 결정한 경우 트랜잭션을 롤백합니다. ROLLBACK 문은 데이터를 트랜잭션이 시작되기 전 상태로 되돌려서 트랜잭션 진행 중 수정된 모든 내용을 취소합니다. ROLLBACK은 또한 트랜잭션에서 보유 중인 리소스를 해제합니다.  
  
> [!NOTE]  
> MARS를 지원하도록 설정된 연결에서는 실행 보류 중인 요청이 있을 경우 API 함수를 통해 시작한 명시적 트랜잭션을 커밋할 수 없습니다. 보류 중인 작업이 있는 동안 이러한 유형의 트랜잭션을 커밋하려고 하면 오류가 발생합니다.  
  
#### <a name="errors-during-transaction-processing"></a>트랜잭션 처리 중 오류  
 오류로 인해 트랜잭션이 성공적으로 완료되지 않은 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 자동으로 트랜잭션을 롤백하고 해당 트랜잭션에 보유 중인 모든 리소스를 해제합니다. 클라이언트와 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스 간의 네트워크 연결이 끊어진 경우 네트워크에서 이 인스턴스에게 연결이 끊어진 것을 알릴 때 해당 연결에서 보류 중인 트랜잭션은 모두 롤백됩니다. 클라이언트 애플리케이션에 오류가 발생하거나 클라이언트 컴퓨터가 다운 또는 다시 시작되는 경우에도 네트워크 연결은 끊어지고 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스는 네트워크에서 연결이 끊어진 것을 확인하면 보류 중인 트랜잭션을 모두 롤백합니다. 클라이언트가 애플리케이션에서 로그오프하면 보류 중인 트랜잭션은 모두 롤백됩니다.  
  
 일괄 처리에서 제약 조건 위반 등 런타임 문 오류가 발생하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 기본적으로 오류를 발생시킨 문만 롤백합니다. 이 동작은 `SET XACT_ABORT` 문을 사용하여 변경할 수 있습니다. `SET XACT_ABORT` ON이 실행된 후에는 모든 런타임 문 오류 발생 시 자동으로 현재 트랜잭션이 롤백됩니다. 구문 오류와 같은 컴파일 오류는 `SET XACT_ABORT` 옵션 설정으로 영향을 받지 않습니다. 자세한 내용은 [SET XACT_ABORT&#40;Transact-SQL&#41;](../t-sql/statements/set-xact-abort-transact-sql.md)를 참조하세요.  
  
 오류가 발생하면 수정 동작(`COMMIT` 또는 `ROLLBACK`)을 애플리케이션 코드에 포함해야 합니다. 트랜잭션 오류를 포함하여 오류를 효과적으로 처리할 수 있는 도구로는 [!INCLUDE[tsql](../includes/tsql-md.md)] `TRY...CATCH` 구문이 있습니다. 트랜잭션이 포함된 예를 보려면 [TRY...CATCH&#40;Transact-SQL&#41;](../t-sql/language-elements/try-catch-transact-sql.md)를 참조하십시오. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터 `THROW` 문을 사용하여 예외를 발생시키고 실행 영역을 `TRY...CATCH` 구문의 `CATCH` 블록으로 넘길 수 있습니다. 자세한 내용은 [THROW&#40;Transact-SQL&#41;](../t-sql/language-elements/throw-transact-sql.md)을 참조하세요.  
  
##### <a name="compile-and-run-time-errors-in-autocommit-mode"></a>자동 커밋 모드에서 컴파일 오류 및 런타임 오류  
 자동 커밋 모드에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스가 한 SQL 문이 아니라 전체 일괄 처리를 롤백하는 것처럼 보일 때가 있습니다. 이러한 상황은 런타임 오류가 아니라 컴파일 오류가 발생했을 때 나타납니다. 컴파일 오류가 발생하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 실행 계획을 작성할 수 없으므로 일괄 처리가 실행되지 않습니다. 오류를 생성한 문 이전의 모든 문이 롤백되는 것처럼 보이지만 오류가 발생하면 일괄 처리의 모든 문이 실행되지 않습니다. 다음 예에서는 컴파일 오류가 발생하여 세 번째 일괄 처리의 `INSERT` 문이 하나도 실행되지 않습니다. 처음 두 `INSERT` 문이 롤백되는 것처럼 보이지만 전혀 실행되지 않은 것입니다.  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUSE (3, 'ccc');  -- Syntax error.  
GO  
SELECT * FROM TestBatch;  -- Returns no rows.  
GO  
```  
  
 다음 예에서는 세 번째 `INSERT` 문에서 런타임 기본 키 중복 오류가 발생합니다. 처음 두 `INSERT` 문은 성공하고 커밋되므로 런타임 오류 이후에도 유지됩니다.  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUES (1, 'ccc');  -- Duplicate key error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 실행 시간까지 개체 이름이 확인되지 않는 지연된 이름 확인 기능을 사용합니다. 다음 예에서는 처음 두 `INSERT` 문이 실행되어 커밋되므로 세 번째 `TestBatch` 문이 존재하지 않는 테이블을 참조하여 런타임 오류를 생성한 후에도 처음 두 행은 `INSERT` 테이블에 유지됩니다.  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBch VALUES (3, 'ccc');  -- Table name error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```   
  
##  <a name="locking-and-row-versioning-basics"></a><a name="Lock_Basics"></a> 잠금 및 행 버전 관리 기본 사항  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 여러 사용자가 동시에 데이터를 액세스하는 경우 다음 메커니즘을 사용하여 트랜잭션의 무결성을 확인하고 데이터베이스의 일관성을 유지합니다.  
  
-  **잠금**    

   각 트랜잭션은 해당 트랜잭션이 종속되는 행, 페이지 또는 테이블 등의 리소스에 대해 서로 다른 유형의 잠금을 요청합니다. 잠금은 다른 트랜잭션의 리소스 수정을 차단하여 잠금을 요청하는 트랜잭션에 문제가 발생하지 않도록 합니다. 각 트랜잭션은 잠긴 리소스에 더 이상 종속되지 않게 되면 잠금을 해제합니다.  
  
-  **행 버전 관리**    

   행 버전 관리 기반 격리 수준을 사용하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 수정된 각 행의 버전을 유지 관리합니다. 애플리케이션에서는 잠금을 사용하여 모든 읽기 작업을 보호하는 대신 트랜잭션이 해당 트랜잭션 또는 쿼리 시작 부분에 있는 행 버전을 사용하여 데이터를 확인하도록 지정할 수 있습니다. 행 버전 관리를 사용하면 읽기 작업에 의해 다른 트랜잭션이 차단될 가능성이 크게 줄어듭니다.  
  
 잠금 및 행 버전 관리는 사용자가 커밋되지 않은 데이터를 읽을 수 없도록 하고 여러 사용자가 동일한 데이터를 동시에 변경하지 못하도록 합니다. 잠금 또는 행 버전 관리를 사용하지 않는 경우 데이터에 대해 쿼리를 실행하면 아직 데이터베이스에서 커밋되지 않은 데이터가 반환되어 예기치 않은 결과가 나타날 수 있습니다.  
  
 애플리케이션에서는 다른 트랜잭션에 의해 수정되지 않도록 트랜잭션을 보호하는 수준을 정의하는 트랜잭션 격리 수준을 선택할 수 있습니다. 개별 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해 테이블 수준 힌트를 지정하여 애플리케이션의 요구 사항에 맞는 동작을 더 적절하게 설정할 수 있습니다.  
  
### <a name="managing-concurrent-data-access"></a>동시 데이터 액세스 관리  
 특정 리소스에 여러 사용자가 동시에 액세스하는 것을 동시 액세스라고 합니다. 동시 데이터 액세스를 위해서는 다른 사용자가 현재 사용하고 있는 리소스를 여러 사용자가 수정하려 할 때 역효과가 발생하지 않도록 하는 메커니즘이 필요합니다.  
  
#### <a name="concurrency-effects"></a>동시성 효과  
 사용자가 데이터를 수정하면 동시에 같은 데이터를 읽거나 수정 중인 다른 사용자에게 영향을 미칠 수 있습니다. 이러한 사용자들을 가리켜 데이터에 동시에 액세스한 사용자라고 합니다. 데이터 스토리지 시스템에 동시성 제어가 없으면 사용자가 다음과 같은 부작용을 겪을 수 있습니다.  
  
-   **업데이트 손실** 
  
     업데이트 손실은 둘 이상의 트랜잭션이 같은 행을 선택한 다음 원래 선택한 값을 기준으로 행을 업데이트할 때 발생합니다. 이때 각 트랜잭션은 다른 트랜잭션을 인식하지 못합니다. 마지막 업데이트가 다른 트랜잭션의 업데이트를 덮어쓰므로 데이터가 손실됩니다.  
  
     예를 들어 두 명의 편집자가 같은 문서를 복사한다고 가정합니다. 각 편집자가 각자 복사본을 변경한 다음 변경된 복사본을 저장하면 원본 문서를 덮어쓰게 됩니다. 변경된 복사본을 마지막으로 저장한 편집자가 다른 편집자의 변경 내용을 덮어씁니다. 한 편집자가 트랜잭션을 마치고 커밋할 때까지 다른 편집자가 파일에 액세스할 수 없도록 하면 이 문제를 해결할 수 있습니다.  
  
-   **커밋되지 않은 종속성(더티 읽기)**  
  
     커밋되지 않은 종속성은 다른 트랜잭션이 업데이트 중인 행을 두 번째 트랜잭션이 선택할 때 발생합니다. 두 번째 트랜잭션이 읽고 있는 데이터는 아직 커밋되지 않았지만 현재 행을 업데이트 중인 트랜잭션에 의해 변경될 수 있습니다.  
  
     예를 들어 한 편집자가 문서를 변경 중이라고 가정합니다. 변경하는 동안 다른 편집자가 그 시점까지 변경된 내용이 모두 포함된 문서를 복사한 다음 문서를 배포합니다. 그런데 첫 번째 편집자가 그때까지 변경한 내용이 잘못되었다고 판단하여 편집 내용을 지우고 문서를 저장합니다. 이 경우 배포된 문서에는 더 이상 존재하지 않으며 무시해야 하는 내용이 포함되어 있습니다. 첫 번째 편집자가 수정 내용을 최종 저장하고 트랜잭션 커밋할 때까지 아무도 변경된 문서를 읽을 수 없도록 하면 이 문제를 해결할 수 있습니다.  
  
-   **일관성 없는 분석(반복하지 않는 읽기)**  
  
     일관성 없는 분석은 두 번째 트랜잭션이 같은 행에 여러 번 액세스하며 이때마다 다른 데이터를 읽을 경우 발생합니다. 일관성 없는 분석은 두 번째 트랜잭션이 읽고 있는 데이터를 다른 트랜잭션이 변경하고 있다는 점에서 커밋되지 않은 종속성과 비슷합니다. 그러나 일관성 없는 분석의 경우 두 번째 트랜잭션이 읽은 데이터는 내용을 변경한 트랜잭션에 의해 커밋된 것입니다. 또한 같은 행을 여러 번 읽어야 하고 매번 정보가 다른 트랜잭션에 의해 변경됩니다. 이를 반복하지 않는 읽기라고 합니다.  
  
     예를 들어 한 편집자가 같은 문서를 두 번 읽는 동안 그 사이에 작성자가 문서를 다시 작성할 수 있습니다. 그러면 편집자가 같은 문서를 두 번째 읽을 때 문서가 변경되어 있습니다. 원래의 읽기는 반복되지 않습니다. 편집자가 마지막으로 문서 읽기를 마칠 때까지 작성자가 문서를 변경하지 못하게 하면 이 문제를 해결할 수 있습니다.  
  
-   **가상 읽기**  
  
     가상 읽기는 두 개의 동일한 쿼리가 실행되고 두 번째 쿼리에서 반환된 행 컬렉션이 다른 경우 발생하는 상황입니다. 아래의 예에서는 이러한 상황이 발생하는 경우를 보여 줍니다. 아래의 두 트랜잭션이 동시에 실행되고 있다고 가정합니다. 두 번째 트랜잭션의 `SELECT` 문이 두 트랜잭션에서 사용하는 데이터를 변경하기 때문에 첫 번째 트랜잭션의 두 `INSERT` 문에서 서로 다른 결과를 반환할 수 있습니다.  
  
    ```sql  
    --Transaction 1  
    BEGIN TRAN;  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    --The INSERT statement from the second transaction occurs here.  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    COMMIT;  
    ```  
  
    ```sql  
    --Transaction 2  
    BEGIN TRAN;  
    INSERT INTO dbo.employee  
      (Id, Name) VALUES(6 ,'New');  
    COMMIT;   
    ```  
  
-   **행 업데이트로 인한 읽기 누락 및 두 번 읽기**  
  
    -   업데이트된 행이 누락되거나 업데이트된 행이 여러 번 표시됨  
  
         `READ UNCOMMITTED` 수준에서 실행되는 트랜잭션은 현재 트랜잭션에서 읽은 데이터를 다른 트랜잭션에서 수정하지 못하도록 하는 공유 잠금을 실행하지 않습니다. READ COMMITTED 수준에서 실행되는 트랜잭션은 공유 잠금을 실행하지만 행을 읽은 후에는 행 또는 페이지 잠금을 해제합니다. 어떤 경우든 인덱스를 검색할 때 사용자가 읽기 작업을 수행하는 동안 다른 사용자가 행의 인덱스 키 열을 변경하면 키 변경으로 인해 사용자가 아직 검색하지 않은 위치로 행이 이동될 경우 해당 행이 다시 나타날 수 있습니다. 마찬가지로 키 변경으로 인해 사용자가 이미 읽은 인덱스 위치로 행이 이동될 경우 해당 행이 나타나지 않을 수 있습니다. 이 문제를 방지하려면 `SERIALIZABLE` 또는 `HOLDLOCK` 힌트 또는 행 버전 관리를 사용합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
    -   업데이트 대상이 아니었던 하나 이상의 행이 누락됨  
  
         `READ UNCOMMITTED`을 사용할 때 사용자 쿼리에서 할당 순서 검색(IAM 페이지 사용)을 사용하여 행을 읽는 경우 다른 트랜잭션에 의해 페이지 분할이 발생하면 행이 누락될 수 있습니다. 페이지 분할 중에 테이블 잠금이 유지되므로 커밋된 읽기를 사용할 때는 누락이 발생하지 않습니다. 또한 업데이트로 인해 페이지 분할이 발생하지 않으므로 테이블에 클러스터형 인덱스가 없는 경우 누락이 발생하지 않습니다.  
  
#### <a name="types-of-concurrency"></a>동시성 유형  
 여러 사용자가 동시에 데이터베이스의 데이터를 수정할 수 있도록 하려면 특정 사용자의 수정 내용이 다른 사용자의 수정 내용에 영향을 주지 않도록 제어 시스템을 구현해야 합니다. 이것을 동시성 제어라고 합니다.  
  
 동시성 제어는 동시성 제어 구현 방법에 따라 두 가지로 분류됩니다.  
  
-   **비관적** 동시성 제어  
  
     다른 사용자에게 영향을 주는 데이터 수정은 수행할 수 없도록 하는 잠금 방식입니다. 한 사용자가 잠금을 유발하는 동작을 수행하면 다른 사용자는 이 소유자가 잠금을 해제할 때까지 해당 잠금과 충돌하는 동작을 수행할 수 없습니다. 이러한 방식은 동시성 충돌이 발생하는 경우 잠금을 사용하여 데이터를 보호하는 비용이 트랜잭션을 롤백하는 비용보다 작고 데이터에 대한 경합이 치열한 환경에 주로 사용되기 때문에 비관적 제어라고 합니다.  
  
-   **낙관적** 동시성 제어  
  
     낙관적 동시성 제어에서는 사용자가 데이터를 읽을 때 해당 데이터를 잠그지 않습니다. 사용자가 데이터를 업데이트할 때는 다른 사용자가 해당 데이터를 읽은 후 변경하지 않았는지 검사가 진행됩니다. 다른 사용자가 데이터를 업데이트한 경우에는 오류가 발생합니다. 일반적으로 오류를 수신한 사용자의 트랜잭션이 롤백되고 다시 시작됩니다. 이러한 방식은 가끔씩 트랜잭션을 롤백하는 비용이 데이터를 읽을 때 잠그는 비용보다 작고 데이터에 대한 경합이 낮은 환경에 주로 사용되기 때문에 낙관적 제어라고 합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 다양한 동시성 제어 유형을 지원합니다. 사용자는 연결에 대한 트랜잭션 격리 수준 또는 커서에 대한 동시성 옵션을 선택하여 동시성 제어 유형을 지정하게 됩니다. 이러한 특성은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용하거나 ADO, ADO.NET, OLE DB 및 ODBC 등의 데이터베이스 API(응용 프로그래밍 인터페이스) 속성과 특성을 통해 정의할 수 있습니다.  
  
#### <a name="isolation-levels-in-the-ssdenoversion"></a>[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 격리 수준  
 한 트랜잭션을 리소스 또는 다른 트랜잭션에서 수정한 데이터 내용으로부터 격리하는 정도를 정의하는 격리 수준을 트랜잭션에 지정할 수 있습니다. 격리 수준은 허용되는 동시성 부작용(예: 커밋되지 않은 읽기 또는 가상 읽기)의 관점에서 설명됩니다.  
  
 트랜잭션 격리 수준으로 제어할 수 있는 사항은 다음과 같습니다.  
  
-   데이터를 읽을 때 잠금을 확보할지 여부 및 요청되는 잠금의 종류  
-   읽기 잠금의 보유 기간  
-   읽기 작업이 다른 트랜잭션에서 수정한 행을 참조할 경우 선택할 수 있는 다음과 같은 옵션  
    -   행에 대한 배타적 잠금이 해제될 때까지 차단  
    -   문 또는 트랜잭션 시작 당시 커밋된 행 버전 검색  
    -   커밋되지 않은 데이터 수정 내용 읽기  
  
> [!IMPORTANT]  
> 트랜잭션 격리 수준을 선택해도 데이터 수정 내용을 보호하기 위해 획득된 잠금에는 영향을 주지 않습니다. 설정된 격리 수준에 관계없이 트랜잭션은 항상 수정하는 데이터에 대해 배타적 잠금을 얻고 해당 트랜잭션이 완료될 때까지 이 잠금을 보유합니다. 읽기 작업의 경우 트랜잭션 격리 수준은 대개 다른 트랜잭션에서 수정한 내용의 영향을 받지 않도록 보호 수준을 정의합니다.  
  
 격리 수준이 낮을수록 동시에 데이터를 액세스할 수 있는 사용자가 많아지지만 동시성 부작용(예: 커밋되지 않은 읽기 또는 업데이트 손실) 횟수도 늘어납니다. 반대로 격리 수준이 높을수록 동시성 부작용 종류가 줄어들지만 시스템 리소스가 더 많이 필요하게 되고 한 트랜잭션이 다른 트랜잭션을 차단하게 될 확률도 높아집니다. 적절한 격리 수준을 선택하려면 애플리케이션의 데이터 무결성 요구 사항과 각 격리 수준에 의해 야기되는 오버헤드를 신중하게 평가해야 합니다. 최상위 격리 수준인 직렬화 가능의 경우 트랜잭션이 읽기 작업을 반복할 때마다 정확히 동일한 데이터를 검색하지만 다중 사용자 시스템에서 다른 사용자에게 영향을 줄 수 있는 수준의 잠금을 수행함으로써 이를 달성합니다. 최하위 격리 수준인 커밋되지 않은 읽기의 경우 다른 트랜잭션에서 수정했지만 커밋되지 않은 데이터를 검색할 수 있습니다. 커밋되지 않은 읽기에서는 모든 동시성 부작용이 발생할 수 있지만 읽기 잠금이나 버전 관리가 수행되지 않으므로 오버헤드가 최소화됩니다.  
  
##### <a name="database-engine-isolation-levels"></a>데이터베이스 엔진 격리 수준  
 ISO 표준은 다음 격리 수준을 정의합니다. 이 격리 수준은 모두 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 지원됩니다.  
  
|격리 수준|정의|  
|---------------------|----------------|  
|**READ UNCOMMITTED**|물리적으로 손상된 데이터만 읽지 않도록 트랜잭션을 격리하는 최하위 격리 수준입니다. 이 수준에서는 더티 읽기가 허용되므로 한 트랜잭션에서 변경한 아직 커밋되지 않은 내용을 다른 트랜잭션에서 볼 수 있습니다.|  
|**READ COMMITTED**|트랜잭션에서는 처음 트랜잭션이 완료될 때까지 기다리지 않고 다른 트랜잭션에서 이전에 읽은 수정되지 않은 데이터를 읽을 수 있습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 트랜잭션이 끝날 때까지 쓰기 잠금이 유지되지만(일부 데이터에서 적용됨) 읽기 잠금은 SELECT 작업이 수행되는 즉시 해제됩니다. 이 값은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 기본 수준입니다.|  
|**REPEATABLE READ**|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 트랜잭션이 끝날 때까지 일부 데이터에서 획득되는 읽기 잠금 및 쓰기 잠금이 유지됩니다. 그러나 범위 잠금이 관리되지 않으므로 가상 읽기가 발생할 수 있습니다.|  
|**직렬화 가능**|트랜잭션이 서로 완전히 격리되는 최상위 수준입니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 일부 데이터에서 획득되는 읽기 잠금 및 쓰기 잠금이 유지되고 트랜잭션이 끝날 때 해제됩니다. 범위 잠금은 SELECT 작업에서 특히 가상 읽기를 방지하기 위해 범위가 지정된 WHERE 절을 사용할 때 필요합니다.<br /><br /> **참고:** 직렬화 가능 격리 수준이 요청된 경우 복제된 테이블에 대한 DDL 작업 및 트랜잭션이 실패할 수 있는데 이는 복제 쿼리가 직렬화 가능 격리 수준과 호환되지 않을 수 있는 힌트를 사용하기 때문입니다.|  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 행 버전 관리를 사용하는 두 개의 추가 트랜잭션 격리 수준을 지원합니다. 하나는 커밋된 읽기 격리를 구현한 것이고 다른 하나는 트랜잭션 격리 수준인 스냅샷입니다.  
  
|행 버전 관리 기반 격리|정의|  
|------------------------------------|----------------|  
|**커밋된 스냅샷 읽기(RCSI)**|READ_COMMITTED_SNAPSHOT 데이터베이스 옵션을 ON으로 설정하면 커밋된 읽기 격리가 행 버전 관리를 통해 문 수준의 읽기 일관성을 제공합니다. 읽기 작업에 SCH-S 테이블 수준 잠금만 필요하고 페이지 또는 행 잠금은 필요하지 않습니다. 즉, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 행 버전 관리를 사용하여 문 시작 시와 트랜잭션별로 데이터의 일관성이 유지된 스냅샷을 각 문에 제공합니다. 다른 트랜잭션에 의한 데이터 업데이트 차단을 위해 잠금이 사용되지는 않습니다. 사용자 정의 함수는 UDF를 포함하는 구문 시간이 시작된 후에 커밋된 데이터를 반환할 수 있습니다.<br /><br /> `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 기본값인 OFF로 설정하면 커밋된 격리 읽기는 공유 잠금을 사용하여 현재 트랜잭션이 읽기 작업을 실행하는 동안 다른 트랜잭션이 행을 수정하지 못하도록 합니다. 또한 공유 잠금은 다른 트랜잭션이 완료될 때까지 해당 트랜잭션이 수정한 행을 문이 읽을 수 없도록 합니다. 두 구현 모두 커밋된 읽기 격리에 대한 ISO 정의를 충족합니다.|  
|**스냅샷**|스냅샷 격리 수준은 행 버전 관리를 통해 트랜잭션 수준의 읽기 일관성을 제공합니다. 읽기 작업에 SCH-S 테이블 잠금만 필요하고 페이지 또는 행 잠금은 필요하지 않습니다. 다른 트랜잭션에서 수정한 행을 읽을 때 트랜잭션 시작 당시의 행 버전을 검색합니다. `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정하면 데이터베이스에 대해 스냅샷 격리만 사용할 수 있습니다. 기본적으로 사용자 데이터베이스에 대해서는 이 옵션이 OFF로 설정되어 있습니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 메타데이터의 버전 관리를 지원하지 않습니다. 따라서 스냅샷 격리에서 실행하는 명시적 트랜잭션에서 수행할 수 있는 DDL 작업에 대한 제한 사항이 있습니다. ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME 또는 CLR(공용 언어 런타임) DDL 문과 같은 DDL 문은 BEGIN TRANSACTION 문 다음에 스냅샷 격리에서 허용되지 않습니다. 다음 명령문은 암시적 트랜잭션 내에서 스냅샷 격리를 사용하는 경우 허용됩니다. 기본적으로 암시적 트랜잭션은 DDL 문에서도 스냅샷 격리의 의미 체계를 적용할 수 있게 하는 단일 문입니다. 이 원칙을 위반하면 오류 3961이 발생할 수 있습니다. `Snapshot isolation transaction failed in database '%.*ls' because the object accessed by the statement has been modified by a DDL statement in another concurrent transaction since the start of this transaction. It is not allowed because the metadata is not versioned. A concurrent update to metadata could lead to inconsistency if mixed with snapshot isolation.`|  
  
 다음 표에서는 각 격리 수준에서 사용되는 동시성 부작용을 보여 줍니다.  
  
|격리 수준|커밋되지 않은 읽기|반복되지 않는 읽기|가상|  
|---------------------|----------------|------------------------|-------------|  
|**READ UNCOMMITTED**|예|예|예|  
|**READ COMMITTED**|예|예|예|  
|**REPEATABLE READ**|예|아니요|예|  
|**스냅샷**|예|예|예|  
|**직렬화 가능**|예|예|예|  
  
 각 트랜잭션 격리 수준에서 제어하는 특정 종류의 잠금 또는 행 버전 관리에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하십시오.  
  
 트랜잭션 격리 수준은 [!INCLUDE[tsql](../includes/tsql-md.md)]이나 데이터베이스 API를 통해 설정할 수 있습니다.  
  
 **[!INCLUDE[tsql](../includes/tsql-md.md)]**                                      
 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트는 `SET TRANSACTION ISOLATION LEVEL` 문을 사용합니다.  
  
 **ADO**  
 ADO 애플리케이션은 **Connection** 개체의 `IsolationLevel` 속성을 adXactReadUncommitted, adXactReadCommitted, adXactRepeatableRead 또는 adXactReadSerializable로 설정합니다.  
  
 **ADO.NET**  
 `System.Data.SqlClient` 관리 네임스페이스를 사용하는 ADO.NET 애플리케이션은 `SqlConnection.BeginTransaction` 메서드를 호출하고 *IsolationLevel* 옵션을 Unspecified, Chaos, ReadUncommitted, ReadCommitted, RepeatableRead, Serializable 및 Snapshot으로 설정할 수 있습니다.  
  
 **OLE DB**  
 OLE DB를 사용하는 애플리케이션은 트랜잭션을 시작할 때 *isoLevel* 을 ISOLATIONLEVEL_READUNCOMMITTED, ISOLATIONLEVEL_READCOMMITTED, ISOLATIONLEVEL_REPEATABLEREAD, ISOLATIONLEVEL_SNAPSHOT 또는 ISOLATIONLEVEL_SERIALIZABLE로 설정하고 `ITransactionLocal::StartTransaction`을 호출합니다.  
  
 OLE DB 애플리케이션은 자동 커밋 모드로 트랜잭션 격리 수준을 지정할 때 DBPROPSET_SESSION 속성인 DBPROP_SESS_AUTOCOMMITISOLEVELS를 DBPROPVAL_TI_CHAOS, DBPROPVAL_TI_READUNCOMMITTED, DBPROPVAL_TI_BROWSE, DBPROPVAL_TI_CURSORSTABILITY, DBPROPVAL_TI_READCOMMITTED, DBPROPVAL_TI_REPEATABLEREAD, DBPROPVAL_TI_SERIALIZABLE, DBPROPVAL_TI_ISOLATED 또는 DBPROPVAL_TI_SNAPSHOT으로 설정할 수 있습니다.  
  
 **ODBC**  
 ODBC 애플리케이션은 *Attribute* 를 SQL_ATTR_TXN_ISOLATION으로 설정하고 *ValuePtr* 을 SQL_TXN_READ_UNCOMMITTED, SQL_TXN_READ_COMMITTED, SQL_TXN_REPEATABLE_READ 또는 SQL_TXN_SERIALIZABLE로 설정하고 `SQLSetConnectAttr`을 호출합니다.  
  
 스냅샷 트랜잭션의 경우 애플리케이션은 Attribute를 SQL_COPT_SS_TXN_ISOLATION으로, ValuePtr을 SQL_TXN_SS_SNAPSHOT으로 설정하고 `SQLSetConnectAttr`을 호출합니다. SQL_COPT_SS_TXN_ISOLATION이나 SQL_ATTR_TXN_ISOLATION을 사용하여 스냅샷 트랜잭션을 검색할 수 있습니다.  
  
##  <a name="locking-in-the-database-engine"></a><a name="Lock_Engine"></a> 데이터베이스 엔진에서의 잠금  
 잠금은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 사용하는 메커니즘으로 동시에 여러 사용자가 동일한 데이터에 액세스하는 것을 동기화합니다.  
  
 특정 트랜잭션이 데이터 읽기나 수정 등을 통해 현재 데이터 상태에 종속되기 전에 동일한 데이터를 수정하는 다른 트랜잭션의 영향을 받지 못하도록 해당 트랜잭션을 보호해야 합니다. 트랜잭션은 데이터에 대한 잠금을 요청하여 자체 트랜잭션을 보호합니다. 잠금에는 공유나 배타 등의 다양한 모드가 있습니다. 잠금 모드는 데이터에 대한 트랜잭션의 종속성 수준을 정의합니다. 해당 데이터에 대해 이미 다른 트랜잭션에 허용된 잠금 모드와 충돌되는 잠금은 이 트랜잭션에 허용될 수 없습니다. 특정 트랜잭션에서 이미 허용된 잠금과 충돌되는 잠금 모드를 동일한 데이터에 요청하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스는 첫 번째 잠금이 해제될 때까지 요청한 트랜잭션을 일시 중지합니다.  
  
 트랜잭션을 통해 데이터를 수정하는 경우 해당 트랜잭션이 끝날 때까지 잠금을 지속하여 수정한 내용이 유지되도록 보호합니다. 읽기 작업을 보호할 수 있도록 획득한 잠금을 트랜잭션에서 지속하는 기간은 트랜잭션 격리 수준 설정에 따라 다릅니다. 트랜잭션을 통해 지속되는 모든 잠금은 트랜잭션이 완료되어 커밋되거나 롤백될 때 해제됩니다.  
  
 일반적으로 애플리케이션은 잠금을 직접 요청하지 않습니다. 잠금은 잠금 관리자라고 하는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 일부를 통해 내부적으로 관리됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스가 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 처리할 때 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 쿼리 프로세서는 액세스할 리소스를 확인합니다. 쿼리 프로세서는 액세스 유형과 트랜잭션 격리 수준 설정에 따라 각 리소스를 보호하는 데 필요한 잠금 유형을 결정합니다. 그런 다음 쿼리 프로세서는 잠금 관리자에게 적절한 잠금을 요청합니다. 잠금 관리자는 다른 트랜잭션에서 지속되는 잠금과 충돌되지 않는 잠금을 허용합니다.  
  
## <a name="lock-granularity-and-hierarchies"></a>잠금 세분성 및 계층  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 한 트랜잭션으로 여러 유형의 리소스를 잠글 수 있는 다양한 세분성의 잠금을 제공합니다. 잠금 비용을 최소화하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 자동으로 태스크에 맞는 수준에서 리소스를 잠급니다. 행과 같이 작은 세분성에서 잠그면 동시성이 향상되지만 많은 행을 잠글 경우 더 많은 잠금을 보유해야 하므로 오버헤드가 늘어납니다. 테이블과 같이 큰 세분성에서 잠그면 전체 테이블이 잠겨 다른 트랜잭션이 테이블에 액세스하지 못하게 제한되므로 동시성은 떨어지지만 유지 관리할 잠금 수가 적으므로 오버헤드가 줄어듭니다.  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]이 리소스를 완전히 보호하기 위해 여러 수준의 세분성에서 잠금을 획득해야 하는 경우가 많습니다. 이러한 여러 수준의 세분성 잠금 그룹을 잠금 계층 구조라고 합니다. 예를 들어 인덱스 읽기를 완전히 보호하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 인스턴스에서는 행에 대한 공유 잠금과 페이지와 테이블에 대한 내재된 공유 잠금을 획득해야 합니다.  
  
 다음 표에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]이 잠글 수 있는 리소스를 보여 줍니다.  
  
|리소스|Description|  
|--------------|-----------------|  
|RID|행 식별자는 힙 내의 단일 행을 잠그는 데 사용됩니다.|  
|KEY|인덱스 내의 행 잠금은 직렬화 가능한 트랜잭션에서 키 범위를 보호하는 데 사용됩니다.|  
|PAGE|데이터 또는 인덱스 페이지와 같은 데이터베이스의 8KB 페이지입니다.|  
|EXTENT|데이터 또는 인덱스 페이지와 같은 인접한 8개의 페이지 그룹입니다.|  
|HoBT|힙 또는 B-트리입니다. 클러스터형 인덱스가 없는 테이블에서 힙 데이터 페이지나 B-트리(인덱스)를 보호하는 잠금입니다.|  
|TABLE|모든 데이터와 인덱스가 포함된 전체 테이블입니다.|  
|FILE|데이터베이스 파일입니다.|  
|APPLICATION|애플리케이션이 지정한 리소스입니다.|  
|METADATA|메타데이터 잠금입니다.|  
|ALLOCATION_UNIT|할당 단위입니다.|  
|DATABASE|전체 데이터베이스입니다.|  
  
> [!NOTE]  
> HoBT 및 TABLE 잠금은 [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)의 LOCK_ESCALATION 옵션의 영향을 받을 수 있습니다.  
  
## <a name="lock-modes"></a><a name="lock_modes"></a> 잠금 모드  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 동시 트랜잭션이 리소스에 액세스할 수 있는 방법을 결정하는 여러 가지 잠금 모드를 사용하여 리소스를 잠급니다.  
  
 다음 표에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 사용하는 리소스 잠금 모드를 보여 줍니다.  
  
|잠금 모드|Description|  
|---------------|-----------------|  
|**공유(S)**|SELECT 문처럼 데이터를 변경하거나 업데이트하지 않는 읽기 작업에 사용합니다.|  
|**업데이트(U)**|업데이트할 수 있는 리소스에 사용합니다. 여러 개의 세션이 리소스를 읽고, 잠그고, 나중에 업데이트할 때 발생하는 일반적인 교착 상태를 방지합니다.|  
|**배타적(X)**|INSERT, UPDATE, DELETE와 같은 데이터 수정 작업에 사용합니다. 여러 개의 업데이트 작업이 같은 리소스에 대해 동시에 이루어지지 못하게 합니다.|  
|**의도**|잠금 계층 구조를 만드는 데 사용합니다. 의도 잠금의 종류에는 내재된 공유(IS), 내재된 배타(IX), 공유 내재된 배타(SIX)가 있습니다.|  
|**스키마**|테이블의 스키마에 종속되는 작업이 실행될 때 사용합니다. 스키마 잠금에는 스키마 수정(Sch-M)과 스키마 안정성(Sch-S) 잠금이 있습니다.|  
|**대량 업데이트(BU)**|데이터를 테이블로 대량 복사하는 경우와 **TABLOCK** 힌트가 지정된 경우에 사용합니다.|  
|**키 범위**|직렬화 가능 트랜잭션 격리 수준을 사용할 때 쿼리가 읽는 행 범위를 보호합니다. 쿼리가 다시 실행될 경우 직렬화 가능 트랜잭션의 쿼리에 대해 반환되는 행을 다른 트랜잭션이 삽입할 수 없도록 합니다.|  
  
### <a name="shared-locks"></a><a name="shared"></a> 공유 잠금  
 공유(S) 잠금을 사용하면 비관적 동시성 제어 하에서 동시 트랜잭션이 리소스를 읽을(SELECT) 수 있습니다. 리소스에 공유(S) 잠금이 설정되어 있는 동안에는 다른 트랜잭션이 데이터를 수정할 수 없습니다. 트랜잭션 격리 수준을 반복 읽기 이상으로 설정하거나 잠금 힌트를 사용하여 트랜잭션 기간에 대한 공유(S) 잠금을 보유하지 않는 한, 리소스에 대한 공유(S) 잠금은 읽기 작업이 완료되면 바로 해제됩니다.  
  
### <a name="update-locks"></a><a name="update"></a> 업데이트 잠금  
 업데이트(U) 잠금을 사용하면 일반적인 형태의 교착 상태가 방지됩니다. 반복 읽기 또는 직렬화 가능 트랜잭션의 경우 트랜잭션이 데이터를 읽고, 리소스(페이지 또는 행)에 대한 공유(S) 잠금을 얻은 다음 데이터를 수정하는데 행을 수정할 때는 배타적(X) 잠금으로 잠금을 변환해야 합니다. 두 트랜잭션이 리소스에 대해 공유 모드 잠금을 얻은 다음 데이터를 동시에 업데이트하려고 하면 한 트랜잭션이 배타적(X) 잠금으로 잠금을 변환하려고 합니다. 한 트랜잭션의 배타 잠금은 다른 트랜잭션의 공유 모드 잠금과 호환되지 않으므로 공유 모드를 배타 모드로 변환할 때는 잠금 대기가 발생합니다. 두 번째 트랜잭션이 해당 업데이트에 대해 배타적(X) 잠금을 얻으려고 합니다. 이 경우 두 트랜잭션 모두 배타적(X) 잠금으로 변환 중이고 각각 상대 트랜잭션이 공유 모드 잠금을 해제하기를 기다리므로 교착 상태가 발생합니다.  
  
 이러한 교착 상태를 방지하려면 업데이트(U) 잠금을 사용합니다. 한 번에 한 트랜잭션만 리소스에 대한 업데이트(U) 잠금을 얻을 수 있습니다. 트랜잭션이 리소스를 수정하면 업데이트(U) 잠금이 배타적(X) 잠금으로 변환됩니다.  
  
### <a name="exclusive-locks"></a><a name="exclusive"></a> 배타 잠금  
 배타적(X) 잠금을 사용하면 동시 트랜잭션이 리소스에 액세스할 수 없습니다. 배타(X) 잠금을 사용하면 다른 트랜잭션이 데이터를 수정할 수 없습니다. 읽기 작업은 NOLOCK 힌트 또는 READ UNCOMMITED 격리 수준을 사용해서만 수행할 수 있습니다.  
  
 INSERT, UPDATE 및 DELETE 등의 데이터 수정 문은 데이터 수정과 읽기 작업을 함께 수행합니다. 해당 문은 먼저 읽기 작업을 수행하여 데이터를 확보한 후 필요한 수정 작업을 수행합니다. 따라서 데이터 수정 문은 대개 공유 잠금과 배타 잠금을 모두 필요로 합니다. 예를 들어 UPDATE 문은 다른 테이블과의 조인이 있는 테이블의 행을 수정할 수 있습니다. 이 경우 UPDATE 문은 조인 테이블에서 읽는 행에 대한 공유 잠금과 업데이트되는 행에 대한 배타 잠금을 함께 요청합니다.  
  
### <a name="intent-locks"></a><a name="intent"></a> 의도 잠금  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 의도 잠금을 사용하여 잠금 계층 구조 아래쪽에 있는 하위 수준 리소스에 설정되는 공유(S) 잠금 또는 배타적(X) 잠금을 보호합니다. 하위 수준의 잠금보다 먼저 확보되어 하위 수준에 잠금을 설정하려고 하는 의도를 나타내므로 의도 잠금이라고 합니다.  
  
 의도 잠금은 다음과 같은 두 가지 역할을 합니다.  
  
-   다른 트랜잭션이 상위 수준 리소스를 수정하여 하위 수준 잠금을 무효화하는 것을 방지합니다. 
-   [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 상위 수준 세분성에서 발생하는 잠금 충돌을 보다 효율적으로 발견할 수 있도록 해 줍니다.  
  
 예를 들어 테이블 내의 페이지 또는 행에 대한 공유(S) 잠금이 요청되기 전에 해당 테이블 수준에서 공유 의도 잠금이 요청됩니다. 테이블 수준에서 의도 잠금을 설정하면 이후에 다른 트랜잭션이 해당 페이지를 포함하는 테이블에 대해 배타적(X) 잠금을 얻을 수 없습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 테이블 수준에서만 의도 잠금을 확인하여 트랜잭션이 해당 테이블에 대해 잠금을 얻을 수 있는지 확인하므로 의도 잠금을 사용하면 성능이 향상됩니다. 이 경우 테이블의 모든 행 또는 페이지 잠금을 확인하여 트랜잭션이 전체 테이블을 잠글 수 있는지 확인할 필요가 없습니다.  
  
<a name="lock_intent_table"></a> 의도 잠금에는 내재된 공유(IS) 잠금, 의도 배타(IX) 잠금, 의도 배타 공유(SIX) 잠금이 있습니다.  
  
|잠금 모드|Description|  
|---------------|-----------------|  
|**내재된 공유(IS)(IS)**|계층 구조의 아래쪽에 있는 일부 리소스에 대해 요청되거나 확보된 공유 잠금을 보호합니다.|  
|**의도 배타(IX)**|계층 구조의 아래쪽에 있는 일부 리소스에 대해 요청되거나 확보된 배타 잠금을 보호합니다. IX는 IS의 상위 집합으로, 하위 수준 리소스에 대한 공유 잠금 요청도 보호합니다.|  
|**의도 배타 공유(SIX)**|계층 구조의 아래쪽에 있는 모든 리소스에 대해 요청되거나 확보된 공유 잠금 및 하위 수준 리소스 일부에 대해 요청되거나 확보된 의도 배타 잠금을 보호합니다. 최상위 수준 리소스에서는 동시 IS 잠금이 허용됩니다. 예를 들어 테이블에 대한 SIX 잠금을 확보하면 수정되는 페이지에 대한 의도 배타 잠금 및 수정되는 행에 대한 배타 잠금도 동시에 확보됩니다. 리소스당 한 번에 하나의 SIX 잠금을 설정할 수 있으므로 다른 트랜잭션이 테이블 수준에서 IS 잠금을 얻어 계층 구조 아래쪽에 있는 리소스를 읽을 수는 있어도 다른 트랜잭션이 리소스를 업데이트할 수는 없습니다.|  
|**의도 업데이트(IU)**|계층 구조 아래쪽에 있는 모든 리소스에 대해 요청되거나 확보된 업데이트 잠금을 보호합니다. IU 잠금은 페이지 리소스에만 사용됩니다. 업데이트 작업이 발생하면 IU 잠금이 IX 잠금으로 변환됩니다.|  
|**공유 의도 업데이트(SIU)**|S 잠금과 IU 잠금이 결합된 것으로, 두 잠금을 별도로 확보한 후 동시에 동시에 보유할 경우 설정됩니다. 예를 들어 트랜잭션이 PAGLOCK 힌트가 있는 쿼리를 실행한 다음 업데이트 작업을 실행하면 PAGLOCK 힌트가 있는 쿼리는 S 잠금을 확보하고 업데이트 작업은 IU 잠금을 확보합니다.|  
|**업데이트 의도 배타(UIX)**|U 잠금과 IX 잠금이 결합된 것으로, 두 잠금을 별도로 확보한 후 동시에 동시에 보유할 경우 설정됩니다.|  
  
### <a name="schema-locks"></a><a name="schema"></a> 스키마 잠금  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 열을 추가하거나 테이블을 삭제하는 등의 테이블 DDL(데이터 정의 언어) 작업 중에 스키마 수정(Sch-M) 잠금을 사용합니다. Sch-M 잠금이 유지되는 동안에는 테이블에 대한 동시 액세스가 방지됩니다. 즉, 잠금이 해제되기 전까지는 Sch-M 잠금이 모든 외부 작업을 차단합니다.  
  
 테이블 잘림 등의 일부 DML(데이터 조작 언어)은 Sch-M 잠금을 사용하여 영향을 받는 테이블에 대한 동시 작업의 액세스를 방지합니다.  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 쿼리를 컴파일하고 실행할 때 스키마 안정성(Sch-S) 잠금을 사용합니다. Sch-S 잠금은 배타적(X) 잠금 등의 트랜잭션 잠금을 차단하지 않습니다. 따라서 쿼리가 컴파일되는 동안 테이블에 대한 X 잠금이 있는 트랜잭션을 포함하여 다른 트랜잭션이 계속 실행됩니다. 그러나 Sch-M 잠금을 획득하는 동시 DML 작업과 동시 DDL 작업은 테이블에서 수행할 수 없습니다.  
  
### <a name="bulk-update-locks"></a><a name="bulk_update"></a> 대량 업데이트 잠금  
 대량 업데이트(BU) 잠금을 사용하면 여러 스레드가 데이터를 동시에 같은 테이블로 대량 로드하는 것은 허용하고, 데이터를 대량 로드하지 않는 다른 프로세스가 테이블에 액세스하는 것은 방지할 수 있습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 다음 조건이 모두 충족되면 대량 업데이트(BU) 잠금을 사용합니다.  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] BULK INSERT 문 또는 OPENROWSET(BULK) 함수를 사용하거나 .NET SqlBulkCopy, OLEDB 빠른 로드 API 또는 ODBC 대량 복사 API와 같은 BULK INSERT 명령 중 하나를 사용하여 데이터를 테이블에 대량 복사합니다.  
-   **TABLOCK** 힌트를 지정하거나 **sp_tableoption** 을 사용하여 **table lock on bulk load** 테이블 옵션을 설정합니다.  
  
> [!TIP]  
> 덜 제한적인 대량 업데이트 잠금을 보유하는 BULK INSERT 문과 달리 TABLOCK 힌트를 사용하는 INSERT INTO...SELECT 문은 테이블에 대해 배타적(X) 잠금을 보유합니다. 즉, 병렬 삽입 작업을 사용하여 행을 삽입할 수 없습니다.  
  
### <a name="key-range-locks"></a><a name="key_range"></a> 키 범위 잠금  
 키 범위 잠금은 직렬화 가능 트랜잭션 격리 수준을 사용하는 동안 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 읽는 레코드 집합에 포함된 행 범위를 암시적으로 보호합니다. 키 범위 잠금은 가상 읽기를 방지합니다. 행 간에 키 범위를 보호하면 트랜잭션이 액세스하는 레코드 집합에 대한 가상 삽입이나 가상 삭제도 방지됩니다.  
  
## <a name="lock-compatibility"></a><a name="lock_compatibility"></a> 잠금 호환성  
 잠금 호환성에 따라 여러 트랜잭션이 동시에 같은 리소스에 대한 잠금을 획득할 수 있는지 여부가 결정됩니다. 이미 다른 트랜잭션에서 리소스를 잠근 경우에는 요청된 잠금 모드가 기존 잠금 모드와 호환되어야만 새 잠금 요청이 허용될 수 있습니다. 요청된 잠금의 모드가 기존 잠금과 호환되지 않을 경우 새 잠금을 요청하는 트랜잭션은 기존 잠금이 해제되거나 잠금 시간 초과 간격이 만료될 때까지 기다립니다. 예를 들어 배타적 잠금과 호환되는 잠금 모드는 없습니다. 배타적(X) 잠금이 설정되어 있는 동안 다른 트랜잭션은 배타적(X) 잠금이 해제될 때까지 해당 리소스에 대해 공유, 업데이트 또는 배타적 잠금을 비롯한 어떠한 유형의 잠금도 획득할 수 없습니다. 리소스에 공유(S) 잠금이 적용된 경우에는 첫 번째 트랜잭션이 완료되지 않아도 다른 트랜잭션이 해당 항목에 대해 공유 잠금 또는 업데이트(U) 잠금을 획득할 수 있습니다. 그러나 공유 잠금이 해제될 때까지는 다른 트랜잭션이 배타적 잠금을 획득할 수 없습니다.  
  
<a name="lock_compat_table"></a> 다음 표에서는 가장 일반적인 잠금 모드의 호환성을 보여줍니다.  
  
||기존의 허가 모드||||||  
|------|---------------------------|------|------|------|------|------|  
|**요청 모드**|**IS**|**S**|**U**|**IX**|**SIX**|**X**|  
|**내재된 공유(IS)(IS)**|예|예|예|예|예|예|  
|**공유(S)**|예|예|예|예|예|예|  
|**업데이트(U)**|예|예|예|예|예|예|  
|**의도 배타(IX)**|예|예|아니요|예|예|예|  
|**의도 배타 공유(SIX)**|예|예|예|예|예|예|  
|**배타적(X)**|예|예|예|예|예|예|  
  
> [!NOTE]  
> 의도 배타(IX) 잠금은 모든 행이 아닌 일부 행만 업데이트하기 위한 것이므로 IX 잠금 모드와 호환됩니다. 일부 행을 읽거나 업데이트하려고 하는 다른 트랜잭션도 허용됩니다. 단, 해당 행을 다른 트랜잭션이 업데이트하고 있지 않아야 합니다. 두 트랜잭션이 같은 행을 업데이트하려고 시도하는 경우 두 트랜잭션 모두에 테이블 및 페이지 수준의 IX 잠금이 부여됩니다. 하지만 한 트랜잭션에 행 수준의 X 잠금이 부여되므로 다른 트랜잭션은 행 수준 잠금이 제거될 때까지 대기해야 합니다.  
  
<a name="lock_matrix"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 모든 잠금 모드의 호환성을 확인하려면 다음 표를 사용합니다.  
  
 ![lock_conflicts](../relational-databases/media/LockConflictTable.png)  
  
## <a name="key-range-locking"></a>키 범위 잠금  
 키 범위 잠금은 직렬화 가능 트랜잭션 격리 수준을 사용하는 동안 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 읽는 레코드 집합에 포함된 행 범위를 암시적으로 보호합니다. 직렬화 가능 격리 수준에서는 트랜잭션 중 실행되는 모든 쿼리가 트랜잭션 중 실행될 때마다 동일한 행 집합을 가져와야 합니다. 키 범위 잠금은 다른 트랜잭션에서 해당 키가 직렬화 가능 트랜잭션에서 읽은 키 범위에 속하는 새 행을 삽입하지 못하도록 하여 이 요구 사항을 보호합니다.  
  
 키 범위 잠금은 가상 읽기를 방지합니다. 또한 행 사이에서 키 범위를 보호하여 트랜잭션에서 액세스하는 레코드 집합에 대한 가상 삽입을 방지합니다.  
  
 키 범위 잠금은 인덱스에 배치되어 시작 키 값과 종료 키 값을 지정합니다. 이 잠금은 키 값이 해당 범위에 속하는 모든 행의 삽입, 업데이트 또는 삭제 시도를 차단합니다. 이는 이러한 작업을 수행하려면 먼저 인덱스에 대한 잠금을 획득해야 하기 때문입니다. 예를 들어 직렬화 가능 트랜잭션은 해당 키 값이 `BETWEEN 'AAA' AND 'CZZ'` 조건과 일치하는 모든 행을 읽는 `SELECT` 문을 실행할 수 있습니다. **'** AAA **'** 부터 **'** CZZ **'** 까지의 범위에 있는 키 값에 대한 키 범위 잠금은 다른 트랜잭션에서 해당 키 값이 **'** ADG **'** , **'** BBD **'** 또는 **'** CAL **'** 과 같이 해당 범위에 있는 행을 삽입하지 못하도록 합니다.  
  
### <a name="key-range-lock-modes"></a><a name="key_range_modes"></a> 키 범위 잠금 모드  
 키 범위 잠금에는 범위-행 형식으로 지정된 범위 및 행 구성 요소가 모두 포함됩니다.  
  
-   범위는 두 개의 연속되는 인덱스 항목 간의 범위를 보호하는 잠금 모드를 나타냅니다.  
-   행은 인덱스 항목을 보호하는 잠금 모드를 나타냅니다.  
-   모드는 사용된 혼합 잠금 모드를 나타냅니다. 키 범위 잠금 모드는 두 부분으로 구성됩니다. 첫 번째는 인덱스 범위(Range *T*)를 잠그는 데 사용하는 잠금 유형을 나타내고 두 번째는 특정 키(*K*)를 잠그는 데 사용하는 잠금 유형을 나타냅니다. 두 부분은 *T*-*K* 와 같이 하이픈(-)으로 연결됩니다.  
  
    |범위|행|Mode|Description|  
    |-----------|---------|----------|-----------------|  
    |RangeS|S|RangeS-S|공유 범위, 공유 리소스 잠금. 직렬화 가능한 범위 검색입니다.|  
    |RangeS|U|RangeS-U|공유 범위, 업데이트 리소스 잠금, 직렬화 가능한 업데이트 검색입니다.|  
    |RangeI|Null|RangeI-N|삽입 범위, null 리소스 잠금. 인덱스에 새 키를 삽입하기 전에 범위를 테스트하는 데 사용됩니다.|  
    |RangeX|X|RangeX-X|배타적 범위, 배타적 리소스 잠금. 범위 내의 키를 업데이트할 때 사용됩니다.|  
  
> [!NOTE]  
> 내부적 Null 잠금 모드는 다른 모든 잠금 모드와 호환됩니다.  
  
 키 범위 잠금 모드에는 겹치는 키 및 범위에서 얻은 다른 잠금과 호환되는 잠금을 보여 주는 호환성 행렬이 있습니다.  
  
||기존의 허가 모드|||||||  
|------|---------------------------|------|------|------|------|------|------|  
|**요청 모드**|**S**|**U**|**X**|**RangeS-S**|**RangeS-U**|**RangeI-N**|**RangeX-X**|  
|**공유(S)**|예|예|아니요|예|예|예|예|  
|**업데이트(U)**|예|예|아니요|예|아니요|예|예|  
|**배타적(X)**|예|예|예|예|아니요|예|예|  
|**RangeS-S**|예|예|아니요|예|예|예|예|  
|**RangeS-U**|예|예|아니요|예|예|예|예|  
|**RangeI-N**|예|예|예|예|아니요|예|예|  
|**RangeX-X**|예|예|예|예|예|예|예|  
  
### <a name="conversion-locks"></a><a name="lock_conversion"></a> 변환 잠금  
 변환 잠금은 키 범위 잠금이 다른 잠금과 겹칠 때 만들어집니다.  
  
|잠금 1|잠금 2|변환 잠금|  
|------------|------------|---------------------|  
|S|RangeI-N|RangeI-S|  
|U|RangeI-N|RangeI-U|  
|X|RangeI-N|RangeI-X|  
|RangeI-N|RangeS-S|RangeX-S|  
|RangeI-N|RangeS-U|RangeX-U|  
  
 변환 잠금은 다양한 복합 환경에서 짧은 시간 동안 나타날 수 있으며 때로는 동시 프로세스를 실행하는 동안에 나타납니다.  
  
### <a name="serializable-range-scan-singleton-fetch-delete-and-insert"></a>직렬화 가능 범위 검색, 단일 인출, 삭제 및 삽입  
 키 범위 잠금을 사용하면 다음 작업을 직렬화할 수 있습니다.  
  
-   범위 검색 쿼리  
-   존재하지 않는 행의 단일 인출  
-   삭제 작업  
-   삽입 작업  
  
 키 범위 잠금이 발생하려면 다음 조건을 만족해야 합니다.  
  
-   트랜잭션 격리 수준을 SERIALIZABLE로 설정해야 합니다.  
-   쿼리 프로세서가 인덱스를 사용하여 범위 필터 조건자를 구현해야 합니다. 예를 들어 SELECT 문의 WHERE 절은 다음 조건자를 사용하여 범위 조건을 설정할 수 있습니다. ColumnX BETWEEN N **'** AAA **'** AND N **'** CZZ **'** . 키 범위 잠금은 **ColumnX** 가 인덱스 키 내에 있는 경우에만 얻을 수 있습니다.  
  
### <a name="examples"></a>예제  
 다음 테이블 및 인덱스는 이어지는 키 범위 잠금 예의 기준으로 사용됩니다.  
  
 ![btree](../relational-databases/media/btree4.png)  
  
#### <a name="range-scan-query"></a>범위 검색 쿼리  
 범위 검색 쿼리가 직렬화 가능인지 확인하려면 같은 트랜잭션 내에서 같은 쿼리를 실행할 때마다 같은 결과를 반환해야 합니다. 다른 트랜잭션에서는 범위 스캔 쿼리 내에 새 행을 추가하면 안됩니다. 그렇지 않으면 이러한 행은 가상 삽입이 됩니다. 예를 들어 다음 쿼리는 앞 그림의 테이블과 인덱스를 사용합니다.  
  
```sql  
SELECT name  
FROM mytable  
WHERE name BETWEEN 'A' AND 'C';  
```  
  
 키 범위 잠금은 이름이 `Adam`과 `Dale` 값 사이에 있는 데이터 행 범위에 해당하는 인덱스 항목에 설정되어 앞의 쿼리에서 한정하는 새 행의 추가 또는 삭제를 방지합니다. 이 범위의 첫 번째 이름은 `Adam`이지만 이 인덱스 항목에 RangeS-S 모드 키 범위 잠금을 사용하면 `Abigail`과 같이 A로 시작하는 새 이름을 `Adam` 앞에 추가할 수 없습니다. 마찬가지로 `Dale`의 인덱스 항목에 RangeS-S 키 범위 잠금을 사용하면 `Clive`와 같이 C로 시작하는 새 이름을 `Carlos` 뒤에 추가할 수 없습니다.  
  
> [!NOTE]  
> 보유한 RangeS-S 잠금 수는 *n*+1입니다. 여기서 *n* 은 쿼리를 만족하는 행 수입니다.  
  
#### <a name="singleton-fetch-of-nonexistent-data"></a>존재하지 않는 데이터의 단일 인출  
 트랜잭션 내의 쿼리가 존재하지 않는 행을 선택하려고 하면 같은 트랜잭션 내에서 나중에 쿼리를 실행해도 같은 결과를 반환해야 합니다. 다른 트랜잭션도 존재하지 않는 행을 삽입할 수 없습니다. 다음과 같은 쿼리를 예로 들 수 있습니다.  
  
```sql  
SELECT name  
FROM mytable  
WHERE name = 'Bill';  
```  
  
 이 경우 `Ben`이라는 이름이 인접한 두 인덱스 항목 사이에 삽입되므로 키 범위 잠금은 `Bing`부터 `Bill`까지의 이름 범위에 해당하는 인덱스 항목에 적용됩니다. RangeS-S 모드 키 범위 잠금은 인덱스 항목 `Bing`에 적용됩니다. 이렇게 되면 다른 모든 트랜잭션이 `Bill` 등의 값을 인덱스 항목 `Ben`과 `Bing` 사이에 삽입할 수 없습니다.  
  
#### <a name="delete-operation"></a>삭제 작업  
 트랜잭션 내에서 값을 삭제할 때는 트랜잭션이 삭제 작업을 수행하는 동안 값이 속하는 범위를 잠글 필요가 없습니다. 삭제된 키 값을 트랜잭션이 끝날 때까지 잠그기만 해도 직렬화 기능이 유지됩니다. 다음과 같은 DELETE 문을 예로 들 수 있습니다.  
  
```sql  
DELETE mytable  
WHERE name = 'Bob';  
```  
  
 배타적(X) 잠금이 `Bob`이라는 이름에 해당하는 인덱스 항목에 설정되어 있습니다. 다른 트랜잭션은 삭제된 값인 `Bob` 전후에 값을 삽입하거나 삭제할 수 있습니다. 그러나 값 `Bob`을 읽거나 삽입하거나 삭제하려는 트랜잭션은 삭제 트랜잭션이 커밋되거나 롤백될 때까지 차단됩니다.  
  
 범위 삭제는 세 가지 기본 잠금 모드인 행 잠금, 페이지 잠금 또는 테이블 잠금을 사용하여 실행될 수 있습니다. 행, 페이지 또는 테이블 잠금 전략은 쿼리 최적화 프로그램에 의해 결정되거나 ROWLOCK, PAGLOCK 또는 TABLOCK 등의 쿼리 최적화 프로그램 힌트를 통해 사용자가 지정할 수 있습니다. PAGLOCK 또는 TABLOCK을 사용하는 경우 이 페이지에서 모든 행이 삭제되면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 즉시 인덱스 페이지 할당을 해제합니다. 반대로 ROWLOCK을 사용하면 삭제된 모든 행이 삭제된 것으로 표시만 되고 나중에 백그라운드 태스크를 사용하여 인덱스 페이지에서 제거됩니다.  
  
#### <a name="insert-operation"></a>삽입 작업  
 트랜잭션 내에서 값을 삽입할 때는 트랜잭션이 삽입 작업을 수행하는 동안 값이 속하는 범위를 잠글 필요가 없습니다. 삽입된 키 값을 트랜잭션이 끝날 때까지 잠그기만 해도 직렬화 기능이 유지됩니다. 다음과 같은 INSERT 문을 예로 들 수 있습니다.  
  
```sql  
INSERT mytable VALUES ('Dan');  
```  
  
 범위를 테스트하기 위해 RangeI-N 모드 키 범위 잠금이 David 이름에 해당하는 인덱스 항목에 적용됩니다. 잠금이 허용되면 `Dan`이 삽입되고 `Dan` 값에 배타적(X) 잠금이 적용됩니다. Range-N 모드 키 범위 잠금은 범위를 테스트하는 데만 필요하며 트랜잭션이 삽입 작업을 수행하는 동안에는 보유되지 않습니다. 다른 트랜잭션은 삽입된 값 `Dan` 전후에 값을 삽입하거나 삭제할 수 있습니다. 그러나 값 `Dan`을 읽거나 삽입하거나 삭제하려는 트랜잭션은 삽입 트랜잭션이 커밋되거나 롤백될 때까지 차단됩니다.  
  
## <a name="lock-escalation"></a>잠금 에스컬레이션
잠금 에스컬레이션은 많은 수의 미세 잠금을 더 적은 수의 성긴 잠금으로 변환하여 동시성 경합 가능성은 높이고 시스템 오버헤드는 줄이는 프로세스입니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]는 하위 수준의 잠금을 획득할 때 더 하위 수준의 개체를 포함하는 개체에 의도 잠금도 배치합니다.

-   행 또는 인덱스 키 범위를 잠그는 경우 [!INCLUDE[ssde_md](../includes/ssde_md.md)]는 행 또는 키를 포함하는 페이지에 의도 잠금을 배치합니다.
-   페이지를 잠그는 경우 [!INCLUDE[ssde_md](../includes/ssde_md.md)]는 페이지를 포함하는 더 상위 수준의 개체에 의도 잠금을 배치합니다. 개체에 배치된 의도 잠금 외에도 다음 개체에 대해 의도 페이지 잠금이 요청됩니다.
    -  비클러스터형 인덱스의 리프 수준 페이지
    -  클러스터형 인덱스의 데이터 페이지
    -  힙 데이터 페이지

[!INCLUDE[ssde_md](../includes/ssde_md.md)]는 동일한 문에 대해 행 잠금과 페이지 잠금을 모두 수행하여 잠금 수를 최소화하고 잠금 에스컬레이션이 필요할 가능성을 낮출 수 있습니다. 예를 들어 데이터베이스 엔진은 비클러스터형 인덱스에는 페이지 잠금을 배치(쿼리를 만족시키기 위해 인덱스 노드에서 충분히 인접한 키가 선택된 경우)하고 데이터에는 행 잠금을 배치할 수 있습니다.

[!INCLUDE[ssde_md](../includes/ssde_md.md)]은 잠금을 에스컬레이션하기 위해 테이블의 의도 잠금을 해당 전체 잠금으로 변경하려고 시도합니다. 예를 들어 의도 배타(IX) 잠금을 배타(X) 잠금으로 변경하거나 내재된 공유(IS) 잠금을 공유(S) 잠금으로 변경하려고 시도합니다. 잠금 에스컬레이션 시도가 성공하여 전체 테이블 잠금을 획득하면 힙이나 인덱스에서 트랜잭션이 보유한 모든 힙 또는 B-트리, 페이지(PAGE) 또는 행 수준(RID) 잠금이 해제됩니다. 전체 잠금을 획득할 수 없는 경우에는 해당 시점에서 잠금 에스컬레이션이 발생하지 않고 데이터베이스 엔진은 행, 키 또는 페이지 잠금 획득을 계속 시도합니다.

[!INCLUDE[ssde_md](../includes/ssde_md.md)]은 행 또는 키 범위 잠금을 페이지 잠금으로 에스컬레이션하지 않고 곧바로 테이블 잠금으로 에스컬레이션합니다. 마찬가지로 페이지 잠금도 항상 테이블 잠금으로 에스컬레이션됩니다. 분할된 테이블의 잠금이 테이블 잠금이 아니라 관련된 파티션에 대한 HoBT 수준으로 에스컬레이션될 수 있습니다. HoBT 수준 잠금이 해당 파티션에 대해 정렬된 HoBT를 반드시 잠그는 것은 아닙니다.

> [!NOTE]
> HoBT 수준 잠금은 일반적으로 동시성을 증가시키지만 각각 다른 파티션을 잠그는 트랜잭션이 배타적 잠금을 다른 파티션으로 확장하려는 경우 교착 상태가 발생할 수도 있습니다. 경우에 따라 TABLE 잠금 세분성이 향상될 수도 있습니다.

동시 트랜잭션이 보유한 잠금의 충돌로 인해 잠금 에스컬레이션 시도가 실패하면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]은 트랜잭션이 획득한 추가 1,250개의 잠금 각각에 대해 잠금 에스컬레이션을 다시 시도합니다.

각 에스컬레이션 이벤트는 주로 단일 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 수준에서 작동합니다. 이벤트가 시작되면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]은 에스컬레이션 임계값 요구 사항이 충족되는 경우 활성 문에서 참조한 테이블 중에서 현재 트랜잭션이 소유한 모든 잠금을 에스컬레이션하려고 시도합니다. 문이 테이블에 액세스하기 전에 에스컬레이션 이벤트가 시작되면 해당 테이블의 잠금에 대한 에스컬레이션은 시도되지 않습니다. 잠금 에스컬레이션이 성공한 경우 테이블이 현재 문에서 참조되고 에스컬레이션 이벤트에 포함되어 있다면 이전 문에서 트랜잭션이 획득하여 이벤트 시작 시에도 여전히 보유하는 모든 잠금이 에스컬레이션됩니다.

예를 들어 다음 작업을 수행하는 세션이 있다고 가정합니다.

-  트랜잭션을 시작합니다.
-  `TableA`를 업데이트합니다. 그러면 TableA에 트랜잭션이 완료될 때까지 보유되는 배타 행 잠금이 생성됩니다.
-  `TableB`를 업데이트합니다. 그러면 TableB에 트랜잭션이 완료될 때까지 보유되는 배타 행 잠금이 생성됩니다.
-  `TableA`와 `TableC`를 조인하는 SELECT를 수행합니다. 쿼리 실행 계획에 따라 행은 `TableC`에서 검색되기 전에 `TableA`에서 검색되어야 합니다.
-  SELECT 문은 `TableC`에 액세스하기 전에 `TableA`에서 행을 검색하는 동안 잠금 에스컬레이션을 트리거합니다.

잠금 에스컬레이션이 성공하면 `TableA`에서 세션이 보유한 잠금만 에스컬레이션됩니다. 여기에는 SELECT 문의 공유 잠금과 이전 UPDATE 문의 배타 잠금이 모두 포함됩니다. 잠금 에스컬레이션을 수행할지 결정하기 위해 세션이 SELECT 문에 대해 `TableA`에서 획득한 잠금 수가 계산되는 동안 에스컬레이션이 성공하면 `TableA`에서 세션이 보유한 모든 잠금은 테이블의 배타 잠금으로 에스컬레이션되고 `TableA`에서 의도 잠금을 포함하여 세분성이 더 낮은 다른 모든 잠금은 해제됩니다.

SELECT 문에 `TableB`에 대한 활성 참조가 없기 때문에 `TableB`의 잠금 에스컬레이션은 시도되지 않습니다. 마찬가지로 에스컬레이션이 발생할 때 아직 액세스되지 않았기 때문에 에스컬레이션되지 않은 `TableC`의 잠금에는 에스컬레이션이 시도되지 않습니다.

### <a name="lock-escalation-thresholds"></a>잠금 에스컬레이션 임계값

잠금 에스컬레이션은 `ALTER TABLE SET LOCK_ESCALATION` 옵션을 사용하여 테이블에서 잠금 에스컬레이션을 사용하지 않도록 설정하지 않은 경우와 다음 조건 중 하나에 해당하는 경우 트리거됩니다.

-  단일 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 분할되지 않은 단일 테이블이나 인덱스에 대해 5,000개 이상의 잠금을 획득한 경우
-  단일 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 분할된 테이블의 단일 파티션에 대해 5,000개 이상의 잠금을 획득하고 `ALTER TABLE SET LOCK_ESCALATION` 옵션이 AUTO로 설정된 경우
-  [!INCLUDE[ssde_md](../includes/ssde_md.md)] 인스턴스의 잠금 수가 메모리 또는 구성 임계값을 초과한 경우

잠금 충돌로 인해 잠금을 에스컬레이션할 수 없는 경우 [!INCLUDE[ssde_md](../includes/ssde_md.md)]은 1,250개의 잠금이 새로 획득될 때마다 주기적으로 잠금 에스컬레이션을 트리거합니다.

### <a name="escalation-threshold-for-a-transact-sql-statement"></a>Transact-SQL 문의 에스컬레이션 임계값
[!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 새로 획득한 잠금 1,250개마다 가능한 에스컬레이션을 검사할 때 잠금 에스컬레이션은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 테이블의 단일 참조에 대해 5,000개 이상의 잠금을 획득한 경우에만 발생합니다. 잠금 에스컬레이션은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 테이블의 단일 참조에 대해 5,000개 이상의 잠금을 획득한 경우 트리거됩니다. 예를 들어 문이 한 인덱스에서 3,000개의 잠금을 획득하고 동일한 테이블의 다른 인덱스에서도 3,000개의 잠금을 획득하는 경우에는 잠금 에스컬레이션이 트리거되지 않습니다. 마찬가지로, 문에 테이블에 대한 자체 조인이 있고 테이블에 대한 각각의 참조가 해당 테이블에서 3,000개의 잠금만 획득하는 경우에는 잠금 에스컬레이션이 트리거되지 않습니다.

잠금 에스컬레이션은 에스컬레이션이 트리거될 때 액세스한 테이블에 대해서만 발생합니다. 단일 SELECT 문이 이 시퀀스에서 `TableA`, `TableB` 및 `TableC`의 3개 테이블에 액세스하는 조인이라고 가정합니다. 이 문은 `TableA`에 대한 클러스터형 인덱스에서 3,000개의 행 잠금을 획득하고 `TableB`에 대한 클러스터형 인덱스에서 5,000개 이상의 행 잠금을 획득하지만 `TableC`에는 아직 액세스하지 않았습니다. [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 이 문이 `TableB`에서 5,000개 이상의 행 잠금을 획득한 것을 검색하면 `TableB`에서 현재 트랜잭션이 보유한 모든 잠금을 에스컬레이션하려고 시도합니다. 또한 `TableA`에서 현재 트랜잭션이 보유한 모든 잠금을 에스컬레이션하려고 시도하지만 `TableA`의 잠금 수가 5,000개 미만이므로 에스컬레이션은 발생하지 않습니다. 에스컬레이션이 발생할 때 아직 액세스되지 않았으므로 `TableC`에 대해서는 잠금 에스컬레이션이 시도되지 않습니다.

### <a name="escalation-threshold-for-an-instance-of-the-database-engine"></a>데이터베이스 엔진 인스턴스의 에스컬레이션 임계값
잠금 수가 잠금 에스컬레이션에 대한 메모리 임계값보다 커지면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 잠금 에스컬레이션을 트리거합니다. 메모리 임계값은 다음과 같은 [잠금 구성 옵션](../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)의 설정에 따라 다릅니다.

-   **잠금** 옵션을 기본값인 0으로 설정하면 잠금 개체에서 사용하는 메모리가 AWE 메모리를 제외하고 데이터베이스 엔진에서 사용하는 메모리의 24%일 때 잠금 에스컬레이션 임계값에 도달합니다. 잠금을 나타내는 데 사용되는 데이터 구조의 길이는 약 100바이트입니다. 데이터베이스 엔진이 다양한 작업에 맞추어 동적으로 메모리를 획득하거나 해제하기 때문에 이 임계값은 동적입니다.

-   **잠금** 옵션을 0 이외의 값으로 설정하면 잠금 에스컬레이션 임계값은 잠금 옵션 값의 40%이고 메모리가 가중되는 경우에는 40% 미만입니다.

[!INCLUDE[ssde_md](../includes/ssde_md.md)]은 에스컬레이션을 수행하기 위해 모든 세션에서 모든 활성 문을 선택할 수 있으며 인스턴스에 사용된 잠금 메모리가 임계값보다 높게 유지되는 경우에는 1,250개의 새 잠금마다 에스컬레이션을 수행할 문을 선택합니다.

### <a name="escalating-mixed-lock-types"></a>혼합 잠금 유형 에스컬레이션
잠금 에스컬레이션이 발생하면 힙이나 인덱스에 대해 선택한 잠금은 더 하위 수준의 가장 제한적인 잠금에 대한 요구 사항도 충분히 만족시킬 수 있습니다.

예를 들어 하나의 세션이 있다고 가정합니다.

-  트랜잭션을 시작합니다.
-  클러스터형 인덱스를 포함하는 테이블을 업데이트합니다.
-  동일한 테이블을 참조하는 SELECT 문을 실행합니다.

UPDATE 문은 다음 잠금을 획득합니다.

-  업데이트된 데이터 행에 대한 배타(X) 잠금
-  이러한 행을 포함하는 클러스터형 인덱스 페이지에 대한 의도 배타(IX) 잠금
-  클러스터형 인덱스에 대한 IX 잠금 및 테이블에 대한 IX 잠금

SELECT 문은 다음 잠금을 획득합니다.

-  행이 UPDATE 문에서 X 잠금으로 아직 보호되지 않은 경우 SELECT 문이 읽는 모든 데이터 행에 대한 공유(S) 잠금
-  페이지가 IX 잠금으로 아직 보호되지 않은 경우 해당 행을 포함하는 모든 클러스터형 인덱스 페이지에 대한 내재된 공유 잠금
-  이미 IX 잠금으로 보호되기 때문에 클러스터형 인덱스나 테이블에 대한 잠금은 없습니다.

SELECT 문이 잠금 에스컬레이션을 트리거하기에 충분한 잠금을 획득하고 에스컬레이션이 성공하면 테이블에 대한 IX 잠금이 X 잠금으로 변환되고 모든 행, 페이지 및 인덱스 잠금이 해제됩니다. 업데이트와 읽기는 모두 테이블에 대한 X 잠금으로 보호됩니다.

### <a name="reducing-locking-and-escalation"></a>잠금 및 에스컬레이션 줄이기
대부분의 경우 [!INCLUDE[ssde_md](../includes/ssde_md.md)]은 잠금 및 잠금 에스컬레이션에 대한 기본 설정으로 작동할 때 최상의 성능을 발휘합니다. [!INCLUDE[ssde_md](../includes/ssde_md.md)] 인스턴스에서 많은 수의 잠금이 생성되고 잠금 에스컬레이션이 자주 발생하면 다음과 같이 잠금 수를 줄이는 것이 좋습니다.

-   읽기 작업에서 공유 잠금을 생성하지 않는 격리 수준 사용:
    -  READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 READ COMMITTED 격리 수준
    -  SNAPSHOT 격리 수준
    -  READ UNCOMMITTED 격리 수준. 이 수준은 커밋되지 않은 읽기로 작동할 수 있는 시스템에서만 사용할 수 있습니다.    
  
    > [!NOTE]
    > 격리 수준 변경은 [!INCLUDE[ssde_md](../includes/ssde_md.md)] 인스턴스의 모든 테이블에 영향을 미칩니다.

-   데이터베이스 엔진이 행 잠금 대신 페이지, 힙 또는 인덱스 잠금을 사용하도록 PAGLOCK 또는 TABLOCK 테이블 힌트 사용. 그러나 이 옵션을 사용하면 한 사용자가 동일한 데이터에 액세스하려는 다른 사용자를 차단하는 문제가 증가하므로 동시 사용자가 많은 시스템에서 이 옵션을 사용하면 안 됩니다.

-   분할된 테이블의 경우 [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)의 LOCK_ESCALATION 옵션을 사용하면 테이블 수준이 아니라 HoBT 수준으로 잠금을 에스컬레이션하거나 잠금 에스컬레이션을 사용하지 않도록 설정할 수 있습니다.

-   큰 일괄 작업을 여러 개의 작은 작업으로 분할합니다. 예를 들어 다음 쿼리를 실행하여 감사 테이블에서 수십만 개의 오래된 레코드를 제거하고, 다른 사용자를 차단하는 잠금 에스컬레이션이 발생했다고 가정합니다.
   
    ```sql
    DELETE FROM LogMessages WHERE LogDate < '2/1/2002'
    ```

    이러한 레코드를 한 번에 수백 개씩 제거하면 트랜잭션당 누적된 잠금 수를 크게 줄이고 잠금 에스컬레이션을 방지할 수 있습니다. 다음은 그 예입니다.

    ```sql
    SET ROWCOUNT 500
    delete_more:
      DELETE FROM LogMessages WHERE LogDate < '2/1/2002'
    IF @@ROWCOUNT > 0 GOTO delete_more
    SET ROWCOUNT 0
    ```

-   쿼리를 최대한 효율적으로 만들어 쿼리 잠금 범위를 좁힙니다. 대규모 검색 또는 대량의 책갈피 조회로 인해 잠금 에스컬레이션 가능성이 증가할 수 있습니다. 또한 교착 상태 가능성이 증가하고, 일반적으로 동시성 및 성능에 부정적인 영향을 미칩니다. 잠금 에스컬레이션을 유발한 쿼리를 찾은 후 새 인덱스를 만들거나 기존 인덱스에 열을 추가하여 인덱스 또는 테이블 검색을 제거하고 인덱스 검색의 효율성을 극대화하는 기회를 찾습니다. [데이터베이스 엔진 튜닝 관리자](../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)를 사용하여 쿼리에 대한 자동 인덱스 분석을 수행하는 것이 좋습니다. 자세한 내용은 [자습서: 데이터베이스 엔진 튜닝 관리자](../tools/dta/tutorial-database-engine-tuning-advisor.md)를 참조하세요.
    이러한 최적화의 한 가지 목표는 인덱스 검색 시 최소한의 행을 반환하여 책갈피 조회 비용을 최소화하는 것입니다(특정 쿼리에 대한 인덱스의 선택도 극대화). [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 책갈피 조회 논리 연산자가 여러 행을 반환할 수 있는 것으로 추정하는 경우 PREFETCH를 사용하여 책갈피 조회를 수행할 수 있습니다. [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 책갈피 조회를 위해 PREFETCH를 사용하는 경우 쿼리 일부의 트랜잭션 격리 수준을 쿼리 일부에 대한 반복 읽기로 높여야 합니다. 이것은 커밋된 읽기 격리 수준에서 SELECT 문과 유사한 것이 (클러스터형 인덱스 및 비클러스터형 인덱스 모두에서) 수천 개의 키 잠금을 획득할 수 있으므로 해당 쿼리가 잠금 에스컬레이션 임계값을 초과하게 될 수 있음을 의미합니다. 이는 에스컬레이션된 잠금이 공유 테이블 잠금이지만 일반적으로 기본값인 커밋된 읽기 격리 수준에서 표시되지 않는 경우에 특히 중요합니다. 책갈피 조회 WITH PREFETCH 절로 인해 에스컬레이션이 발생하는 경우 쿼리 계획의 책갈피 조회 논리 연산자 아래에 있는 인덱스 검색(Seek) 또는 인덱스 검색(Scan) 논리 연산자에 표시되는 비클러스터형 인덱스에 열을 추가하는 것이 좋습니다. 포함 인덱스(쿼리에 사용된 테이블의 모든 열을 포함하는 인덱스) 또는 조인 조건이나 WHERE 절(선택 열 목록에 모든 것을 포함하는 것이 불가능한 경우)에 사용된 열을 포함하는 인덱스를 만들 수 있습니다.
    중첩 루프 조인은 PREFETCH를 사용할 수도 있으며, 이로 인해 동일한 잠금 동작이 발생합니다.
   
-   다른 SPID가 호환되지 않는 테이블 잠금을 보유하고 있는 경우 잠금 에스컬레이션이 발생할 수 없습니다. 잠금 에스컬레이션은 항상 테이블 잠금으로 에스컬레이션되지만 페이지 잠금으로는 에스컬레이션되지 않습니다. 추가로 다른 SPID에 호환되지 않은 TAB 잠금이 있어 잠금 에스컬레이션 시도가 실패하는 경우 에스컬레이션을 시도하는 쿼리가 TAB 잠금을 대기하는 동안 차단하지 않습니다. 대신 더욱 세분화된 수준(행, 키 또는 페이지)에서 계속 잠금을 획득하여 주기적으로 에스컬레이션을 시도합니다. 따라서 특정 테이블에 대한 잠금 에스컬레이션을 방지하는 한 가지 방법은 에스컬레이션된 잠금 유형과 호환되지 않는 다른 연결에 대한 잠금을 획득하고 유지하는 것입니다. 테이블 수준에서 IX(의도 배타) 잠금은 행 또는 페이지를 잠그지 않지만 에스컬레이션된 S(공유) 또는 X(배타) TAB 잠금과 호환되지 않습니다. 예를 들어 mytable 테이블에서 다수의 행을 수정하고 잠금 에스컬레이션으로 인해 발생하는 차단을 유발한 일괄 작업을 실행해야 한다고 가정합니다. 이 작업이 항상 1시간 이내에 완료되는 경우 다음 코드를 포함하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 작업을 만들고, 일괄 작업의 시작 시간 몇 분 전에 시작되도록 새 작업을 예약할 수 있습니다.
  
    ```sql
    BEGIN TRAN
    SELECT * FROM mytable (UPDLOCK, HOLDLOCK) WHERE 1=0
    WAITFOR DELAY '1:00:00'
    COMMIT TRAN
    ```
   
    이 쿼리는 1시간 동안 mytable에 대한 IX 잠금을 획득 및 유지하고, 이로 인해 이 시간 동안 테이블에 대한 잠금 에스컬레이션이 방지됩니다. 이 일괄 처리는 데이터를 수정하거나 다른 쿼리를 차단하지 않습니다(다른 쿼리에서 TABLOCK 힌트를 사용한 테이블 잠금을 적용하지 않는 경우 또는 관리자가 sp_indexoption 저장 프로시저를 사용하여 페이지 또는 행 잠금을 사용하지 않도록 설정한 경우).

추적 플래그 1211 및 1224를 사용하여 잠금 에스컬레이션의 전부 또는 일부를 해제할 수도 있습니다. 하지만 [추적 플래그](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)는 전체 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에 대해 전역으로 모든 잠금 에스컬레이션을 사용하지 않도록 설정합니다. 잠금 에스컬레이션은 수천 개의 잠금을 획득하고 해제하는 오버헤드로 인해 저하되는 쿼리의 효율성을 극대화하여 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 매우 유용한 용도로 사용됩니다. 잠금 에스컬레이션은 잠금을 추적하는 데 필요한 메모리를 최소화하는 경우에도 도움이 됩니다. [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 잠금 구조에 대해 동적으로 할당할 수 있는 메모리는 유한하므로 잠금 에스컬레이션을 사용하지 않도록 설정하고 잠금 메모리가 충분히 커지면 모든 쿼리에 대한 추가 잠금 할당 시도가 실패할 수 있으며 다음 오류가 발생합니다.

```Error: 1204, Severity: 19, State: 1
The SQL Server cannot obtain a LOCK resource at this time. Rerun your statement when there are fewer active users or ask the system administrator to check the SQL Server lock and memory configuration.
```

> [!NOTE]
> [오류 1204](../relational-databases/errors-events/mssqlserver-1204-database-engine-error.md)가 발생하면 현재 문의 처리를 중지하고 활성 트랜잭션 롤백을 유발합니다. 데이터베이스 서비스를 다시 시작하는 경우 롤백 자체가 사용자를 차단하거나 데이터베이스 복구 시간이 길어질 수 있습니다.

> [!NOTE]
> ROWLOCK과 같은 잠금 힌트를 사용하면 초기 잠금 계획만 변경됩니다. 잠금 힌트는 잠금 에스컬레이션을 방지하지 않습니다. 

또한 다음 예제와 같이 `lock_escalation` xEvent(확장 이벤트)를 사용하여 잠금 에스컬레이션을 모니터링합니다.

```sql
-- Session creates a histogram of the number of lock escalations per database 
CREATE EVENT SESSION [Track_lock_escalation] ON SERVER 
ADD EVENT sqlserver.lock_escalation(SET collect_database_name=(1),collect_statement=(1)
    ACTION(sqlserver.database_id,sqlserver.database_name,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,sqlserver.sql_text,sqlserver.username))
ADD TARGET package0.histogram(SET source=N'sqlserver.database_id')
GO
```

> [!IMPORTANT]
> SQL 추적 또는 SQL 프로파일러의 Lock:Escalation 이벤트 클래스 대신 `lock_escalation` xEvent(확장 이벤트)를 사용해야 합니다.

## <a name="dynamic-locking"></a><a name="dynamic_locks"></a> 동적 잠금
 행 잠금과 같이 낮은 수준의 잠금을 사용하면 두 트랜잭션이 동일한 데이터에 대해 동시에 잠금을 요청할 확률이 줄어들어 동시성이 증가합니다. 또한 잠금 수 및 잠금 관리에 필요한 리소스 수도 늘어납니다. 테이블 또는 페이지 잠금과 같이 높은 수준의 잠금을 사용하면 오버헤드는 줄어들지만 동시성이 감소합니다.  
  
 ![잠금 비용 대 동시성 비용](../relational-databases/media/lockcht.png) 
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 동적 잠금 전략을 사용하여 가장 비용 효율적인 잠금을 결정합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 스키마 및 쿼리의 특징을 기준으로 쿼리를 실행할 때 가장 적합한 잠금을 자동으로 결정합니다. 예를 들어 잠금 오버헤드를 줄이기 위해서 인덱스 검색을 수행할 때 최적화 프로그램이 인덱스에서 페이지 수준 잠금을 선택할 수 있습니다.  
  
 동적 잠금을 사용하면 다음과 같은 장점이 있습니다.  
  
-   데이터베이스 관리가 간단해집니다. 데이터베이스 관리자가 잠금 에스컬레이션 임계값을 조정할 필요가 없습니다.  
-   성능이 향상됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 태스크에 적합한 잠금을 사용하므로 시스템 오버헤드가 줄어듭니다.  
-   애플리케이션 개발자가 개발에만 전념할 수 있습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 잠금을 자동으로 조정합니다.  
  
 [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)]부터 `LOCK_ESCALATION` 옵션이 도입되어 잠금 에스컬레이션 동작이 변경되었습니다. 자세한 내용은 [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)의 `LOCK_ESCALATION` 옵션을 참조하세요. 
   
## <a name="deadlocks"></a><a name="deadlocks"></a> 교착 상태  
 한 태스크에서 잠근 리소스를 다른 태스크에서 잠그려고 하여 둘 이상의 태스크가 서로 영구적으로 차단하면 교착 상태가 발생합니다. 예를 들면 다음과 같습니다.  
  
-   트랜잭션 A가 1행에 대한 공유 잠금을 획득합니다.  
-   트랜잭션 B가 2행에 대한 공유 잠금을 획득합니다.  
-   이제 트랜잭션 A가 2행에 대한 배타적 잠금을 요청하고 트랜잭션 B가 2행에 대해 소유하고 있는 공유 잠금을 종료 및 해제할 때까지 트랜잭션 A가 차단됩니다.  
-   이제 트랜잭션 B가 1행에 대한 배타적 잠금을 요청하고 트랜잭션 A가 1행에 대해 소유하고 있는 공유 잠금을 종료 및 해제할 때까지 트랜잭션 B가 차단됩니다.  
  
 트랜잭션 B가 완료되어야 트랜잭션 A도 완료될 수 있지만 트랜잭션 B는 트랜잭션 A에 의해 차단된 상태입니다. 이러한 상태를 순환 종속 관계라고 합니다. 트랜잭션 A는 트랜잭션 B에 종속되고 트랜잭션 B는 트랜잭션 A에 종속된 형태로 순환됩니다.  
  
 교착 상태의 트랜잭션은 둘 다 외부 프로세스에서 교착 상태를 해제할 때까지 기다립니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 교착 상태 모니터는 교착 상태에 있는 태스크가 있는지 주기적으로 검사합니다. 순환 종속 관계가 발견되면 모니터는 두 작업 중 처리하지 않을 태스크를 하나 선택하고 해당 트랜잭션을 오류와 함께 종료합니다. 이렇게 하여 다른 태스크가 해당 트랜잭션을 완료할 수 있습니다. 오류와 함께 종료된 트랜잭션의 애플리케이션은 해당 트랜잭션을 다시 시도하며 이 트랜잭션은 대개 교착 상태의 다른 트랜잭션이 완료된 후에 끝납니다.  
  
 교착 상태는 종종 일반적인 차단과 혼동됩니다. 트랜잭션이 다른 트랜잭션에서 잠근 리소스에 대한 잠금을 요청하면 잠금이 해제될 때까지 잠금을 요청한 트랜잭션이 기다립니다. 기본적으로 LOCK_TIMEOUT이 설정되지 않은 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 트랜잭션 시간은 제한되지 않습니다. 잠금을 요청하는 트랜잭션은 잠금을 소유하는 트랜잭션을 차단하기 위한 작업을 수행하지 않으므로 교착 상태에 빠지지 않고 차단됩니다. 결국 잠금을 소유하는 트랜잭션이 완료되고 잠금을 해제하면 잠금을 요청하는 트랜잭션에 잠금이 허가되고 트랜잭션이 진행됩니다.  
  
> [!NOTE]
> 교착 상태는 deadly embrace(치명적인 포옹)라고도 합니다.  
  
 교착 상태는 관계형 데이터베이스 관리 시스템뿐만 아니라 다중 스레드를 사용하는 어느 시스템에서나 발생할 수 있으며 데이터베이스 개체에 대한 잠금 이외의 리소스에 대해 발생할 수 있습니다. 예를 들어 다중 스레드 운영 체제의 스레드는 메모리 블록과 같은 하나 이상의 리소스를 획득할 수 있습니다. 획득하려는 리소스를 현재 다른 스레드가 소유하고 있으면 대상 리소스가 해제될 때까지 첫 번째 스레드가 기다려야 할 수 있습니다. 이렇게 대기 중인 스레드는 해당 리소스에 대해 리소스를 소유하는 스레드에 종속됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 인스턴스에서 세션은 메모리나 스레드 등의 데이터베이스가 아닌 리소스를 획득할 때 교착 상태에 빠질 수 있습니다.  
  
 ![트랜잭션 교착 상태를 보여 주는 다이어그램](../relational-databases/media/deadlock.png)  
  
 이 그림에서 트랜잭션 T1은 `Part` 테이블 잠금 리소스에 대해 트랜잭션 T2에 종속됩니다. 마찬가지로 스레드 T2는 `Supplier` 테이블 잠금 리소스에 대해 트랜잭션 T1에 종속됩니다. 이러한 종속 관계는 순환적이므로 스레드 T1과 T2 간에 교착 상태가 발생합니다.  
  
 테이블이 분할되고 `ALTER TABLE`의 `LOCK_ESCALATION` 설정이 AUTO로 설정된 경우에도 교착 상태가 발생할 수 있습니다. `LOCK_ESCALATION`이 AUTO로 설정되면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 TABLE 수준이 아니라 HoBT 수준에서 테이블 파티션을 잠그도록 허용하여 동시성이 증가합니다. 그러나 개별 트랜잭션이 테이블에 파티션 잠금을 보유하고 다른 트랜잭션 파티션에서 잠금을 원하면 교착 상태가 발생합니다. 이런 유형의 교착 상태는 `LOCK_ESCALATION`을 `TABLE`로 설정하면 방지할 수 있습니다. 하지만 이 설정으로 인해 테이블 잠금을 기다리도록 파티션에 대규모 업데이트가 강제 적용되어 동시성이 감소됩니다.  
  
### <a name="detecting-and-ending-deadlocks"></a>교착 상태 검색 및 종료  
 한 태스크에서 잠근 리소스를 다른 태스크에서 잠그려고 하여 둘 이상의 태스크가 서로 영구적으로 차단하면 교착 상태가 발생합니다. 다음 그래프에서는 아래와 같은 교착 상태를 개괄적으로 보여 줍니다.  
  
-   태스크 T1이 리소스 R1에 대한 잠금을 가지고 있고(R1에서 T1 방향의 화살표로 표시) 리소스 R2에 대한 잠금을 요청합니다(T1에서 R2 방향의 화살표로 표시).  
-   태스크 T2가 리소스 R2에 대한 잠금을 가지고 있고(R2에서 T2 방향의 화살표로 표시) 리소스 R1에 대한 잠금을 요청합니다(T2에서 R1 방향의 화살표로 표시).  
-   리소스가 사용 가능한 상태가 되어야 태스크를 계속할 수 있고 태스크가 계속되어야 리소스를 해제할 수 있으므로 교착 상태가 발생합니다.  
  
 ![교착 상태에 있는 태스크를 보여 주는 다이어그램](../relational-databases/media/Task_Deadlock_State.png)  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 교착 상태 순환을 자동으로 검색합니다. 그런 다음 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 교착 상태에 있는 세션 중 처리하지 않을 세션을 하나 선택하면 현재 트랜잭션이 오류와 함께 종료되면서 교착 상태가 해제됩니다.  
  
#### <a name="resources-that-can-deadlock"></a><a name="deadlock_resources"></a> 교착 상태를 일으킬 수 있는 리소스  
 사용자 세션마다 세션을 위해 실행 중인 태스크가 하나 이상 있고 각 태스크는 다양한 리소스를 획득하거나 획득 대기 중일 수 있습니다. 다음 유형의 리소스가 차단을 일으켜 교착 상태가 발생할 수 있습니다.  
  
-   **잠금**. 개체, 페이지, 행, 메타데이터, 애플리케이션 등의 리소스에 대한 잠금을 획득하려고 대기할 때 교착 상태가 발생할 수 있습니다. 예를 들어 트랜잭션 T1이 r1 행에 대한 공유(S) 잠금을 가지고 있고 r2에 대한 배타적(X) 잠금을 얻으려고 대기 중입니다. 트랜잭션 T2가 r2에 대한 공유(S) 잠금을 가지고 있고 r1 행에 대한 배타적(X) 잠금을 얻으려고 대기 중입니다. 이 경우 T1과 T2가 서로 잠근 리소스를 해제할 때까지 대기하는 잠금 순환이 발생합니다.  
  
-   **작업자 스레드**. 사용 가능한 작업자 스레드를 대기하는 태스크가 교착 상태를 일으킬 수 있습니다. 대기 태스크가 모든 작업자 스레드를 차단하는 리소스를 소유하는 경우 교착 상태가 발생합니다. 예를 들어 세션 S1이 트랜잭션을 시작하고 r1 행에 대한 공유(S) 잠금을 획득한 후 중지됩니다. 사용 가능한 모든 작업자 스레드에서 실행 중인 활성 세션이 r1 행에 대한 배타적(X) 잠금을 획득하려고 합니다. 세션 S1이 작업자 스레드를 획득할 수 없으므로 트랜잭션을 커밋할 수 없고 r1 행에 대한 잠금을 해제하지 못합니다. 이로 인해 교착 상태가 발생합니다.  
  
-   **메모리**. 동시 요청이 사용 가능한 메모리보다 많은 메모리 부여를 대기하는 경우 교착 상태가 발생할 수 있습니다. 예를 들어 두 개의 동시 쿼리 Q1과 Q2가 각각 10MB와 20MB의 메모리를 획득하는 사용자 정의 함수를 실행합니다. 각 쿼리에 30MB가 필요하고 사용 가능한 총 메모리는 20MB인 경우 Q1과 Q2는 서로 메모리를 해제할 때까지 대기해야 하며 이로 인해 교착 상태가 발생합니다.  
  
-   **병렬 쿼리 실행 관련 리소스**. 일반적으로 교환 포트와 관련된 코디네이터, 생산자 및 소비자 스레드가 병렬 쿼리에 속하지 않는 하나 이상의 다른 프로세스를 포함하는 경우 서로 차단하여 교착 상태가 발생할 수 있습니다. 또한 병렬 쿼리 실행을 시작할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 현재 작업을 기반으로 병렬 처리 수준, 즉 작업자 스레드 수를 결정합니다. 예를 들어 서버에서 새 쿼리 실행이 시작되거나 시스템에 작업자 스레드가 부족하여 시스템 작업이 예기치 않게 변경되면 교착 상태가 발생할 수 있습니다.  
  
-   **MARS(Multiple Active Result Sets) 리소스**. MARS 리소스는 MARS에서 여러 활성 요청의 인터리브를 제어하는 데 사용합니다. 자세한 내용은 [MARS(Multiple Active Result Sets) 사용](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.  
  
    -   **사용자 리소스**. 스레드가 사용자 애플리케이션에서 제어하는 리소스를 대기할 때 해당 리소스는 외부 또는 사용자 리소스로 간주되고 잠금처럼 처리됩니다.  
  
    -   **세션 뮤텍스**. 한 세션에서 실행되고 있는 태스크가 인터리브됩니다. 이는 세션에서 한 태스크만 실행할 수 있음을 나타냅니다. 세션 뮤텍스를 배타적으로 사용할 수 있어야 태스크가 실행될 수 있습니다.  
  
    -   **트랜잭션 뮤텍스**. 한 트랜잭션에서 실행되고 있는 가 인터리브됩니다. 이는 트랜잭션에서 한 태스크만 실행할 수 있음을 나타냅니다. 트랜잭션 뮤텍스를 배타적으로 사용할 수 있어야 태스크가 실행될 수 있습니다.  
  
     MARS에서 태스크가 빠르게 실행되려면 태스크가 세션 뮤텍스를 획득해야 합니다. 태스크가 트랜잭션에서 실행되고 있는 경우에는 트랜잭션 뮤텍스를 획득해야 합니다. 이를 통해 지정된 세션과 지정된 트랜잭션에서 한 번에 한 태스크만 활성화되도록 할 수 있습니다. 필요한 뮤텍스가 획득되면 태스크가 실행될 수 있습니다. 태스크가 완료되거나 요청 중간에 취소되면 태스크는 뮤텍스를 획득할 때와는 반대의 순서로 먼저 트랜잭션 뮤텍스를 해제하고 세션 뮤텍스를 해제합니다. 그러나 이러한 리소스에서 교착 상태가 발생할 수 있습니다. 다음 코드 예제에서는 사용자 요청 U1과 사용자 요청 U2라는 두 태스크가 같은 세션에서 실행되고 있습니다.  
  
    ```  
    U1:    Rs1=Command1.Execute("insert sometable EXEC usp_someproc");  
    U2:    Rs2=Command2.Execute("select colA from sometable");  
    ```  
  
     사용자 요청 U1에서 실행되는 저장 프로시저가 세션 뮤텍스를 획득합니다. 저장 프로시저를 실행하는 데 시간이 오래 걸리면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 저장 프로시저가 사용자 입력을 대기하고 있는 것으로 간주합니다. 사용자가 사용자 요청 U2의 결과 집합을 대기하는 동안 U2는 세션 뮤텍스를 대기하고 U1은 사용자 리소스를 대기합니다. 다음 그림에서는 이 교착 상태를 논리적으로 보여 줍니다.  
  
 ![LogicFlowExamplec](../relational-databases/media/udb9_LogicFlowExamplec.png)  
  
### <a name="deadlock-detection"></a><a name="deadlock_detection"></a> 교착 상태 검색  
 위의 섹션에서 나열한 리소스는 모두 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 교착 상태 검색 스키마에 포함됩니다. 교착 상태 검색은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스의 모든 태스크에 대한 검색을 주기적으로 시작하는 잠금 모니터에서 수행합니다. 다음은 검색 프로세스에 대한 설명입니다.  
  
-   기본 간격은 5초입니다.  
-   잠금 모니터 스레드가 교착 상태를 발견하면 잠금 상태의 빈도에 따라 5초에서 최하 100밀리초까지 교착 상태 검색 간격이 짧아집니다.  
-   잠금 모니터 스레드가 교착 상태 검색을 중지하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 검색 간격을 5초로 늘립니다.  
-   교착 상태가 검색되면 잠금을 대기해야 하는 다음 스레드가 교착 상태 순환에 들어가는 것으로 간주됩니다. 교착 상태 검색 후 처음 두 번의 잠금 대기에서 다음 교착 상태 검색 간격을 대기하지 않고 교착 상태 검색을 즉시 트리거합니다. 예를 들어 현재 간격이 5초일 경우 교착 상태가 검색되면 다음 잠금 대기에서 교착 상태 검색기를 즉시 시작합니다. 교착 상태에 속할 경우 이 잠금 대기는 다음 교착 상태 검색 전에 바로 검색됩니다.  
  
 일반적으로 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 주기적인 교착 상태 검색만 수행합니다. 시스템에서 발생하는 교착 상태 수는 대개 적으므로 주기적인 교착 상태 검색을 통해 시스템의 교착 상태 검색 오버헤드를 줄일 수 있습니다.  
  
 특정 스레드에 대해 교착 상태 검색을 시작할 때 잠금 모니터는 스레드가 대기하고 있는 리소스를 확인합니다. 그런 다음 잠금 모니터는 해당 리소스의 소유자를 찾은 후 순환을 발견할 때까지 이러한 스레드에 대한 교착 상태 검색을 반복적으로 수행합니다. 이러한 방법을 통해 확인된 순환으로 교착 상태가 일어납니다.  
  
 교착 상태가 검색되면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 교착 상태에 있는 스레드 중 처리하지 않을 스레드를 하나 선택하여 교착 상태를 끝냅니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 스레드에 대해 실행되고 있는 현재 일괄 처리를 종료하고 해당 트랜잭션을 롤백한 후 애플리케이션에 1205 오류를 반환합니다. 처리하지 않도록 선택된 스레드의 트랜잭션이 롤백되면 이 트랜잭션에서 보유하는 모든 잠금이 해제됩니다. 이를 통해 다른 스레드의 트랜잭션이 차단 해제되고 계속됩니다. 1205 교착 상태 미처리 오류는 교착 상태와 관련된 스레드와 리소스에 대한 정보를 오류 로그에 기록합니다.  
  
 기본적으로 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 롤백 비용이 가장 저렴한 트랜잭션을 실행하는 세션을 처리하지 않도록 선택합니다. 또는 사용자가 `SET DEADLOCK_PRIORITY` 문을 사용하여 교착 상태에 있는 세션의 우선 순위를 지정할 수 있습니다. DEADLOCK_PRIORITY를 LOW, NORMAL 또는 HIGH로 설정하거나 -10에서 10 사이의 정수 값으로 설정할 수 있습니다. 교착 상태 우선 순위는 기본적으로 NORMAL입니다. 두 세션의 교착 상태 우선 순위가 다르면 교착 상태 우선 순위가 낮은 세션이 처리하지 않을 세션으로 선택됩니다. 두 세션의 교착 상태 우선 순위가 같으면 롤백 비용이 가장 저렴한 트랜잭션의 세션이 선택됩니다. 교착 상태 순환과 관련된 세션의 교착 상태 우선 순위와 비용이 같으면 임의의 세션이 선택됩니다.  
  
 CLR를 사용할 경우 교착 상태 모니터는 관리 프로시저 내부에서 액세스하는 모니터, 판독기/기록기 잠금, 스레드 조인 등의 동기화 리소스에 대한 교착 상태를 자동으로 검색합니다. 그러나 처리하지 않도록 선택된 프로시저에서 예외가 발생하면 교착 상태가 해결됩니다. 처리하지 않도록 선택된 프로시저에서 현재 소유하고 있는 리소스가 예외를 통해 자동으로 해제되지는 않습니다. 리소스는 명시적으로 해제해야 합니다. 예외 동작에 따라 처리하지 않도록 선택된 프로시저를 확인하는 데 사용되는 예외를 찾아 해제할 수 있습니다.  
  
### <a name="deadlock-information-tools"></a><a name="deadlock_tools"></a> 교착 상태 정보 도구  
 교착 상태 정보를 표시하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 SQL Profiler에서 교착 상태 그래프 이벤트와 두 개의 추적 플래그 system\_health xEvent session 형식으로 모니터링 도구를 제공합니다.  

#### <a name="deadlock-extended-event"></a><a name="deadlock_xevent"></a> 교착 상태 확장 이벤트
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터 SQL 추적 또는 SQL Profiler의 교착 상태 그래프 이벤트 클래스 대신 `xml_deadlock_report` 확장 이벤트(xEvent)를 사용해야 합니다.

또한 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이상에서는 교착 상태가 발생할 때 **_system\_health_* _ 세션이 이미 교착 상태 그래프가 포함된 `xml_deadlock_report` xEvent를 모두 캡처합니다. _system\_health* 세션은 기본적으로 사용되므로, 교착 상태 정보를 캡처하기 위해 별도의 xEvent 세션을 구성하지 않아도 됩니다. 

교착 상태 그래프에는 일반적으로 세 개의 서로 다른 노드가 있습니다.
-   **victim-list**. 교착 상태 희생자 프로세스 식별자.
-   **process-list**. 교착 상태와 관련된 모든 프로세스에에 관한 정보입니다.
-   **resource-list**. 교착 상태와 관련된 리소스에 관한 정보입니다.

system\_health 세션 파일 또는 링 버퍼를 열어 `xml_deadlock_report` xEvent가 기록되면 [!INCLUDE[ssManStudio](../includes/ssManStudio-md.md)]는 다음 예에서 볼 수 있듯이 교착 상태와 관련된 작업과 리소스를 그래픽으로 표시합니다. 

![xEvent 교착 상태 그래프](../relational-databases/media/udb9_xEventDeadlockGraphc.png)

다음 쿼리는 *system\_health* 세션 링 버퍼를 통해 캡처된 교착 상태 이벤트를 모두 표시할 수 있습니다.

```sql
SELECT xdr.value('@timestamp', 'datetime') AS [Date],
    xdr.query('.') AS [Event_Data]
FROM (SELECT CAST([target_data] AS XML) AS Target_Data
            FROM sys.dm_xe_session_targets AS xt
            INNER JOIN sys.dm_xe_sessions AS xs ON xs.address = xt.event_session_address
            WHERE xs.name = N'system_health'
              AND xt.target_name = N'ring_buffer'
    ) AS XML_Data
CROSS APPLY Target_Data.nodes('RingBufferTarget/event[@name="xml_deadlock_report"]') AS XEventData(xdr)
ORDER BY [Date] DESC
```

[!INCLUDE[ssResult](../includes/ssresult-md.md)]

![system_health_xevent_query_result](../relational-databases/media/system_health_qry.png)

다음 예제는 위 결과의 첫 번째 링크를 클릭한 후 출력을 보여줍니다.

```xml
<event name="xml_deadlock_report" package="sqlserver" timestamp="2018-02-18T08:26:24.698Z">
  <data name="xml_report">
    <type name="xml" package="package0" />
    <value>
      <deadlock>
        <victim-list>
          <victimProcess id="process27b9b0b9848" />
        </victim-list>
        <process-list>
          <process id="process27b9b0b9848" taskpriority="0" logused="0" waitresource="KEY: 5:72057594214350848 (1a39e6095155)" waittime="1631" ownerId="11088595" transactionname="SELECT" lasttranstarted="2018-02-18T00:26:23.073" XDES="0x27b9f79fac0" lockMode="S" schedulerid="9" kpid="15336" status="suspended" spid="62" sbid="0" ecid="0" priority="0" trancount="0" lastbatchstarted="2018-02-18T00:26:22.893" lastbatchcompleted="2018-02-18T00:26:22.890" lastattention="1900-01-01T00:00:00.890" clientapp="SQLCMD" hostname="ContosoServer" hostpid="7908" loginname="CONTOSO\user" isolationlevel="read committed (2)" xactid="11088595" currentdb="5" lockTimeout="4294967295" clientoption1="538968096" clientoption2="128056">
            <executionStack>
              <frame procname="AdventureWorks2016CTP3.dbo.p1" line="3" stmtstart="78" stmtend="180" sqlhandle="0x0300050020766505ca3e07008ba8000001000000000000000000000000000000000000000000000000000000">
SELECT c2, c3 FROM t1 WHERE c2 BETWEEN @p1 AND @p1+    </frame>
              <frame procname="adhoc" line="4" stmtstart="82" stmtend="98" sqlhandle="0x020000006263ec01ebb919c335024a072a2699958d3fcce60000000000000000000000000000000000000000">
unknown    </frame>
            </executionStack>
            <inputbuf>
SET NOCOUNT ON
WHILE (1=1) 
BEGIN
    EXEC p1 4
END
   </inputbuf>
          </process>
          <process id="process27b9ee33c28" taskpriority="0" logused="252" waitresource="KEY: 5:72057594214416384 (e5b3d7e750dd)" waittime="1631" ownerId="11088593" transactionname="UPDATE" lasttranstarted="2018-02-18T00:26:23.073" XDES="0x27ba15a4490" lockMode="X" schedulerid="6" kpid="5584" status="suspended" spid="58" sbid="0" ecid="0" priority="0" trancount="2" lastbatchstarted="2018-02-18T00:26:22.890" lastbatchcompleted="2018-02-18T00:26:22.890" lastattention="1900-01-01T00:00:00.890" clientapp="SQLCMD" hostname="ContosoServer" hostpid="15316" loginname="CONTOSO\user" isolationlevel="read committed (2)" xactid="11088593" currentdb="5" lockTimeout="4294967295" clientoption1="538968096" clientoption2="128056">
            <executionStack>
              <frame procname="AdventureWorks2016CTP3.dbo.p2" line="3" stmtstart="76" stmtend="150" sqlhandle="0x03000500599a5906ce3e07008ba8000001000000000000000000000000000000000000000000000000000000">
UPDATE t1 SET c2 = c2+1 WHERE c1 = @p    </frame>
              <frame procname="adhoc" line="4" stmtstart="82" stmtend="98" sqlhandle="0x02000000008fe521e5fb1099410048c5743ff7da04b2047b0000000000000000000000000000000000000000">
unknown    </frame>
            </executionStack>
            <inputbuf>
SET NOCOUNT ON
WHILE (1=1) 
BEGIN
    EXEC p2 4
END
   </inputbuf>
          </process>
        </process-list>
        <resource-list>
          <keylock hobtid="72057594214350848" dbid="5" objectname="AdventureWorks2016CTP3.dbo.t1" indexname="cidx" id="lock27b9dd26a00" mode="X" associatedObjectId="72057594214350848">
            <owner-list>
              <owner id="process27b9ee33c28" mode="X" />
            </owner-list>
            <waiter-list>
              <waiter id="process27b9b0b9848" mode="S" requestType="wait" />
            </waiter-list>
          </keylock>
          <keylock hobtid="72057594214416384" dbid="5" objectname="AdventureWorks2016CTP3.dbo.t1" indexname="idx1" id="lock27afa392600" mode="S" associatedObjectId="72057594214416384">
            <owner-list>
              <owner id="process27b9b0b9848" mode="S" />
            </owner-list>
            <waiter-list>
              <waiter id="process27b9ee33c28" mode="X" requestType="wait" />
            </waiter-list>
          </keylock>
        </resource-list>
      </deadlock>
    </value>
  </data>
</event>
```

자세한 내용은 [system_health 세션 사용](../relational-databases/extended-events/use-the-system-health-session.md)을 참조하세요.

#### <a name="trace-flag-1204-and-trace-flag-1222"></a><a name="deadlock_traceflags"></a> 추적 플래그 1204 및 추적 플래그 1222  
 교착 상태가 발생하면 추적 플래그 1204와 추적 플래그 1222는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 오류 로그에 캡처된 정보를 반환합니다. 추적 플래그 1204는 교착 상태와 관련된 각 노드에 의해 형식이 지정된 교착 상태 정보를 보고합니다. 추적 플래그 1222는 프로세스별 및 리소스별 순서로 교착 상태 정보의 형식을 지정합니다. 두 추적 플래그에서 동일한 교착 상태 이벤트의 두 가지 표현을 가져오도록 설정할 수 있습니다.  

> [!IMPORTANT]
> 워크로드가 많고 교착 상태가 발생하는 시스템에서는 추적 플래그 1204와 1222를 사용하지 않는 것이 좋습니다. 이러한 추적 플래그를 사용하면 성능 문제가 발생할 수 있습니다. 대신, 교착 상태 확장 이벤트(#deadlock_xevent)를 사용합니다.
  
 다음 표에서는 추적 플래그 1204 및 1222의 속성 정의 외에도 두 추적 플래그의 유사점과 차이점을 보여 줍니다.  
  
|속성|추적 플래그 1204 및 추적 플래그 1222|추적 플래그 1204만 해당|추적 플래그 1222만 해당|  
|--------------|-----------------------------------------|--------------------------|--------------------------|  
|출력 형식|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 오류 로그에 출력이 캡처됩니다.|교착 상태와 관련된 노드에 초점을 둡니다. 각 노드에 해당하는 섹션이 있으며 마지막 섹션에서 교착 상태에 대해 설명합니다.|XSD(XML 스키마 정의) 스키마를 따르지 않는 XML과 유사한 형식으로 정보를 반환합니다. 형식은 3가지 주요 섹션으로 이루어져 있습니다. 첫 번째 섹션에서는 교착 상태를 선언합니다. 두 번째 섹션에서는 교착 상태와 관련된 각 프로세스에 대해 설명합니다. 세 번째 섹션에서는 추적 플래그 1204의 노드와 같은 리소스에 대해 설명합니다.|  
|식별 특성|**SPID:<x\> ECID:<x\>.** 병렬 프로세스의 경우 시스템 프로세스 ID 스레드를 식별합니다. `SPID:<x> ECID:0` 항목은 주 스레드를 나타냅니다. 여기서 <x\>는 SPID 값으로 대체됩니다. `SPID:<x> ECID:<y>` 항목은 동일한 SPID의 하위 스레드를 나타냅니다. 여기서 <x\>는 SPID 값으로 대체되고 <y\>는 0보다 큽니다.<br /><br /> **BatchID**(추적 플래그 1222의 경우 **sbid**). 잠금을 요청하거나 보유하고 있는 코드 실행이 속한 일괄 처리를 식별합니다. MARS(Multiple Active Result Sets)가 해제되어 있으면 BatchID 값은 0입니다. MARS가 설정되어 있으면 활성 일괄 처리 값은 1에서 *n* 사이입니다. 세션에 활성 일괄 처리가 없는 경우 BatchID는 0입니다.<br /><br /> **모드**. 스레드가 요청, 부여 또는 대기한 특정 리소스에 대한 잠금 유형을 지정합니다. Mode는 IS(내재된 공유), S(공유), U(업데이트), IX(의도 배타), SIX(의도 배타 공유) 및 X(배타)가 될 수 있습니다.<br /><br /> **Line #** (추적 플래그 1222의 경우 **line**). 현재 문 일괄 처리에서 교착 상태 발생 시 실행 중이었던 줄 번호를 나열합니다.<br /><br /> **Input Buf** (추적 플래그 1222의 경우 **inputbuf**). 현재 일괄 처리에 있는 모든 문을 나열합니다.|**노드**. 교착 상태 체인에서 항목 번호를 나타냅니다.<br /><br /> **목록**. 잠금 소유자는 다음 목록에 포함될 수 있습니다.<br /><br /> **Grant List**. 리소스의 현재 소유자를 열거합니다.<br /><br /> **Convert List**. 잠금을 더 높은 수준으로 변환 중인 현재 소유자를 열거합니다.<br /><br /> **Wait List**. 리소스에 대한 현재 새 잠금 요청을 열거합니다.<br /><br /> **Statement Type**. 스레드에 사용 권한이 있는 DML 문의 유형(SELECT, INSERT, UPDATE 또는 DELETE)에 대해 설명합니다.<br /><br /> **Victim Resource Owner**. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 교착 상태 순환을 끊도록 선택되는 참여하는 스레드를 지정합니다. 선택된 스레드와 기존의 모든 하위 스레드가 종료됩니다.<br /><br /> **Next Branch**. 교착 상태 순환과 관련된 동일한 SPID의 하위 스레드 두 개 이상을 나타냅니다.|**deadlock victim**. 교착 상태에 있는 태스크 중 처리하지 않도록 선택된 태스크의 실제 메모리 주소를 나타냅니다. [sys.dm_os_tasks&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)를 참조하십시오. 해결되지 않은 교착 상태의 경우 이 속성이 0일 수 있습니다. 롤백하고 있는 태스크를 처리하지 않도록 선택할 수는 없습니다.<br /><br /> **executionstack**. 교착 상태 발생 시 실행 중인 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드를 나타냅니다.<br /><br /> **priority**. 교착 상태 우선 순위를 나타냅니다. 특정 경우에 동시성 향상을 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 잠시 교착 상태 우선 순위를 바꿀 수 있습니다.<br /><br /> **logused**. 태스크에서 사용하는 로그 공간입니다.<br /><br /> **소유자 ID**. 요청을 제어하는 트랜잭션의 ID입니다.<br /><br /> **상태**. 태스크의 상태입니다. 다음 값 중 하나입니다.<br /><br /> >> **보류 중**. 작업자 스레드 대기 중입니다.<br /><br /> >> **실행 가능**. 실행 준비가 완료되었지만 퀀텀 대기 중입니다.<br /><br /> >> **실행**. 현재 스케줄러에서 실행 중입니다.<br /><br /> >> **일시 중지됨**. 실행이 일시 중지되었습니다.<br /><br /> >> **완료**. 태스크가 완료되었습니다.<br /><br /> >> **spinloop**. spinlock이 사용 가능할 때까지 대기합니다.<br /><br /> **waitresource**. 태스크에 필요한 리소스입니다.<br /><br /> **waittime**. 리소스 대기 시간(밀리초)입니다.<br /><br /> **schedulerid**. 이 태스크와 관련된 스케줄러입니다. [sys.dm_os_schedulers&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md) 참조.<br /><br /> **hostname**. 워크스테이션의 이름입니다.<br /><br /> **isolationlevel**. 현재 트랜잭션 격리 수준입니다.<br /><br /> **Xactid**. 요청을 제어하는 트랜잭션의 ID입니다.<br /><br /> **currentdb**. 데이터베이스의 ID입니다.<br /><br /> **lastbatchstarted**. 클라이언트 프로세스에서 일괄 처리 실행을 마지막으로 시작한 시간입니다.<br /><br /> **lastbatchcompleted**. 클라이언트 프로세스에서 일괄 처리 실행을 마지막으로 완료한 시간입니다.<br /><br /> **clientoption1 및 clientoption2**. 이 클라이언트 연결의 옵션을 설정합니다. 대개 SET NOCOUNT와 SET XACTABORT 등의 SET 문으로 제어하는 옵션에 대한 정보가 포함된 비트 마스크입니다.<br /><br /> **associatedObjectId**. HoBT(힙 또는 B-트리) ID를 나타냅니다.|  
|리소스 특성|**RID**. 잠금이 보유 또는 요청된 테이블 내의 단일 행을 식별합니다. RID는 RID로 표시됩니다. *db_id:file_id:page_no:row_no*. 예들 들어 `RID: 6:1:20789:0`입니다.<br /><br /> **OBJECT**. 잠금이 보유 또는 요청된 테이블을 식별합니다. OBJECT는 OBJECT로 표시됩니다. *db_id:object_id*. 예들 들어 `TAB: 6:2009058193`입니다.<br /><br /> **KEY**. 잠금이 보유 또는 요청된 인덱스 내의 키 범위를 식별합니다. KEY는 KEY로 표시됩니다. *db_id:hobt_id* (*index key hash value*). 예들 들어 `KEY: 6:72057594057457664 (350007a4d329)`입니다.<br /><br /> **PAG**. 잠금이 보유 또는 요청된 페이지 리소스를 식별합니다. PAG는 PAG로 표시됩니다. *db_id:file_id:page_no*. 예들 들어 `PAG: 6:1:20789`입니다.<br /><br /> **EXT**. 익스텐트 구조를 식별합니다. EXT는 EXT로 표시됩니다. *db_id:file_id:extent_no*. 예들 들어 `EXT: 6:1:9`입니다.<br /><br /> **DB**. 데이터베이스 잠금을 식별합니다. **DB는 다음 방법 중 하나로 표시됩니다.**<br /><br /> DB: *db_id*<br /><br /> DB: *db_id*[BULK-OP-DB]. 이 방법은 백업 데이터베이스에서 수행된 데이터베이스 잠금을 식별합니다.<br /><br /> DB: *db_id*[BULK-OP-LOG]. 이 방법은 특정 데이터베이스에 대해 백업 로그에서 수행된 잠금을 식별합니다.<br /><br /> **APP**. 애플리케이션 리소스에서 수행된 잠금을 식별합니다. APP는 APP로 표시됩니다. *lock_resource*. 예들 들어 `APP: Formf370f478`입니다.<br /><br /> **METADATA**. 교착 상태와 관련된 메타데이터 리소스를 나타냅니다. METADATA에는 많은 하위 리소스가 있으므로 반환되는 값은 교착 상태가 발생한 하위 리소스에 따라 달라집니다. 예를 들어 METADATA.USER_TYPE는 `user_type_id =` <*integer_value*>를 반환합니다. METADATA 리소스 및 하위 리소스에 대한 자세한 내용은 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)를 참조하십시오.<br /><br /> **HOBT**. 교착 상태와 관련된 힙 또는 B-트리를 나타냅니다.|이 추적 플래그에만 관련된 사항이 없습니다.|이 추적 플래그에만 관련된 사항이 없습니다.|  
  
##### <a name="trace-flag-1204-example"></a>추적 플래그 1204 예  
 다음 예에서는 추적 플래그 1204가 설정되어 있을 때의 출력을 보여 줍니다. 이 경우 노드 1의 테이블은 인덱스가 없는 힙이고 노드 2의 테이블은 비클러스터형 인덱스가 있는 힙입니다. 노드 2의 인덱스 키는 교착 상태 발생 시 업데이트 중입니다.  
  
```  
Deadlock encountered .... Printing deadlock information  
Wait-for graph  
  
Node:1  
  
RID: 6:1:20789:0               CleanCnt:3 Mode:X Flags: 0x2  
 Grant List 0:  
   Owner:0x0315D6A0 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:55 ECID:0 XactLockInfo: 0x04D9E27C  
   SPID: 55 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
BEGIN TRANSACTION  
   EXEC usp_p2  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x03A3DAD0   
     Mode: U SPID:54 BatchID:0 ECID:0 TaskProxy:(0x04976374) Value:0x315d200 Cost:(0/868)  
  
Node:2  
  
KEY: 6:72057594057457664 (350007a4d329) CleanCnt:2 Mode:X Flags: 0x0  
 Grant List 0:  
   Owner:0x0315D140 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:54 ECID:0 XactLockInfo: 0x03A3DAF4  
   SPID: 54 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
     BEGIN TRANSACTION  
       EXEC usp_p1  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
  
Victim Resource Owner:  
 ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
```  
  
##### <a name="trace-flag-1222-example"></a>추적 플래그 1222 예  
 다음 예에서는 추적 플래그 1222가 설정되어 있을 때의 출력을 보여 줍니다. 이 경우 한 테이블은 인덱스가 없는 힙이고 다른 테이블은 비클러스터형 인덱스가 있는 힙입니다. 두 번째 테이블의 인덱스 키는 교착 상태 발생 시 업데이트 중입니다.  
  
```  
deadlock-list  
 deadlock victim=process689978  
  process-list  
   process id=process6891f8 taskpriority=0 logused=868   
   waitresource=RID: 6:1:20789:0 waittime=1359 ownerId=310444   
   transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:42.733 XDES=0x3a3dad0   
   lockMode=U schedulerid=1 kpid=1952 status=suspended spid=54   
   sbid=0 ecid=0 priority=0 transcount=2   
   lastbatchstarted=2005-09-05T11:22:42.733   
   lastbatchcompleted=2005-09-05T11:22:42.733   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310444 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2016.dbo.usp_p1 line=6 stmtstart=202   
     sqlhandle=0x0300060013e6446b027cbb00c69600000100000000000000  
     UPDATE T2 SET COL1 = 3 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600856aa70f503b8104000000000000000000000000  
     EXEC usp_p1       
    inputbuf  
      BEGIN TRANSACTION  
       EXEC usp_p1  
   process id=process689978 taskpriority=0 logused=380   
   waitresource=KEY: 6:72057594057457664 (350007a4d329)     
   waittime=5015 ownerId=310462 transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:44.077 XDES=0x4d9e258 lockMode=U   
   schedulerid=1 kpid=3024 status=suspended spid=55 sbid=0 ecid=0   
   priority=0 transcount=2 lastbatchstarted=2005-09-05T11:22:44.077   
   lastbatchcompleted=2005-09-05T11:22:44.077   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310462 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2016.dbo.usp_p2 line=6 stmtstart=200   
     sqlhandle=0x030006004c0a396c027cbb00c69600000100000000000000  
     UPDATE T1 SET COL1 = 4 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600d688e709b85f8904000000000000000000000000  
     EXEC usp_p2       
    inputbuf  
      BEGIN TRANSACTION  
        EXEC usp_p2      
  resource-list  
   ridlock fileid=1 pageid=20789 dbid=6 objectname=AdventureWorks2016.dbo.T2   
   id=lock3136940 mode=X associatedObjectId=72057594057392128  
    owner-list  
     owner id=process689978 mode=X  
    waiter-list  
     waiter id=process6891f8 mode=U requestType=wait  
   keylock hobtid=72057594057457664 dbid=6 objectname=AdventureWorks2016.dbo.T1   
   indexname=nci_T1_COL1 id=lock3136fc0 mode=X   
   associatedObjectId=72057594057457664  
    owner-list  
     owner id=process6891f8 mode=X  
    waiter-list  
     waiter id=process689978 mode=U requestType=wait  
```  
  
#### <a name="profiler-deadlock-graph-event"></a>프로파일러 교착 상태 그래프 이벤트  
교착 상태와 관련된 태스크 및 리소스를 그림으로 설명하는 SQL Profiler의 이벤트입니다. 다음 예에서는 교착 상태 그래프 이벤트가 설정되어 있을 때 SQL Profiler의 출력을 보여 줍니다.  
  
 ![ProfilerDeadlockGraphc](../relational-databases/media/udb9_ProfilerDeadlockGraphc.png)  
  
교착 상태 이벤트에 대한 자세한 내용은 [Lock:Deadlock 이벤트 클래스](../relational-databases/event-classes/lock-deadlock-event-class.md)를 참조하세요.

SQL 프로필러 교착 상태 그래프를 실행하는 방법에 대한 자세한 내용은 [교착 상태 그래프 저장&#40;SQL Server 프로파일러&#41;](../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)을 참조하세요.  
  
### <a name="handling-deadlocks"></a>교착 상태 처리  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에서 교착 상태의 트랜잭션 중 처리하지 않을 트랜잭션이 선택되면 현재 배치가 종료되고 해당 트랜잭션이 롤백된 후 애플리케이션에 오류 메시지 1205가 반환됩니다.  
  
 `Your transaction (process ID #52) was deadlocked on {lock | communication buffer | thread} resources with another process and has been chosen as the deadlock victim. Rerun your transaction.`  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리를 전달하는 모든 애플리케이션은 교착 상태에서 처리되지 않을 수 있으므로 애플리케이션에 오류 메시지 1205를 트래핑할 수 있는 오류 처리기가 있어야 합니다. 애플리케이션에서 오류를 트래핑하지 않으면 해당 트랜잭션이 롤백된 것을 모르고 계속 진행하여 오류가 발생할 수 있습니다.  
  
 오류 메시지 1205를 트래핑하는 오류 처리기를 구현하면 애플리케이션에서 교착 상황을 처리하고 자동으로 교착 상태와 관련된 쿼리를 다시 전송하는 등의 동작을 취할 수 있습니다. 쿼리를 자동으로 다시 전송하므로 사용자는 교착 상태가 발생한 것을 알 필요가 없습니다.  
  
 쿼리를 다시 전송하기 전에 애플리케이션이 일시 중지되어야 합니다. 이때 교착 상태와 관련된 다른 트랜잭션이 완료되어 교착 상태의 원인이 되는 해당 잠금을 해제할 수 있습니다. 이를 통해 다시 전송하는 쿼리에서 잠금을 요청할 때 교착 상태가 다시 발생할 가능성을 최소화할 수 있습니다.  
  
### <a name="minimizing-deadlocks"></a><a name="deadlock_minimizing"></a> 교착 상태 최소화  
 교착 상태를 완전히 피할 수는 없지만 특정 코딩 규칙을 따르면 교착 상태가 발생하는 기회를 최소화할 수 있습니다. 교착 상태를 최소화하면 트랜잭션 처리량이 늘어나고 더 적은 수의 트랜잭션이 다음과 같이 되므로 시스템 오버헤드가 줄어듭니다.  
  
-   롤백되어 트랜잭션에 의해 수행된 모든 작업이 실행 취소됩니다.  
-   교착 상태 발생 시 롤백되었으므로 애플리케이션에 의해 다시 전송됩니다.  
  
 교착 상태를 최소화하려면  
  
-   같은 순서로 개체에 액세스합니다.  
-   트랜잭션에서 사용자 상호 작용을 피합니다.  
-   트랜잭션을 하나의 일괄 처리로 짧게 유지합니다.  
-   낮은 격리 수준을 사용합니다.  
-   행 버전 관리 기반의 격리 수준을 사용합니다.  
    -   `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 ON으로 설정하여 커밋된 읽기 트랜잭션이 행 버전 관리를 사용할 수 있도록 합니다.  
    -   스냅샷 격리를 사용합니다.  
-   바인딩된 연결을 사용합니다.  
  
#### <a name="access-objects-in-the-same-order"></a>같은 순서로 개체에 액세스합니다.  
 모든 동시 트랜잭션이 같은 순서로 개체에 액세스하면 교착 상태의 발생 가능성이 줄어듭니다. 예를 들어 두 개의 동시 트랜잭션이 **Supplier** 테이블에 대해 잠금을 얻은 다음, **Part** 테이블에 대해 잠금을 얻으면 다른 트랜잭션이 완료될 때까지 한 트랜잭션이 **Supplier** 테이블에서 차단됩니다. 첫 번째 트랜잭션이 커밋되거나 롤백된 후 두 번째가 계속되므로 교착 상태는 발생하지 않습니다. 모든 데이터 수정에 대해 저장 프로시저를 사용하면 개체 액세스 순서를 표준화할 수 있습니다.  
  
 ![deadlock2](../relational-databases/media/dedlck2.png)  
  
#### <a name="avoid-user-interaction-in-transactions"></a>트랜잭션에서 사용자 상호 작용을 피합니다.  
 사용자 개입 없이 실행되는 일괄 처리의 속도는 애플리케이션의 매개 변수 요청 프롬프트에 대한 응답 등 사용자가 수동으로 쿼리에 응답해야 하는 경우의 속도에 비해 매우 빠르므로 사용자 상호 작용을 포함하는 트랜잭션은 작성하지 않는 것이 좋습니다. 예를 들어 트랜잭션이 사용자 입력을 기다리고 있는데 사용자가 식사를 하러 가거나 퇴근한 경우 사용자는 트랜잭션을 완료할 수 없습니다. 이 경우 트랜잭션에서 보유한 잠금은 트랜잭션이 커밋 또는 롤백되어야 해제되므로 시스템 처리량이 줄어듭니다. 교착 상태가 발생하지 않아도 같은 리소스에 액세스하는 다른 트랜잭션은 해당 트랜잭션이 완료될 때까지 차단됩니다.  
  
#### <a name="keep-transactions-short-and-in-one-batch"></a>트랜잭션을 하나의 일괄 처리로 짧게 유지  
 교착 상태는 보통 오래 실행되는 여러 개의 트랜잭션이 같은 데이터베이스에서 동시에 실행될 때 발생합니다. 트랜잭션 실행 시간이 길수록 배타적 또는 업데이트 잠금 보유 시간이 길어지므로 다른 작업을 차단하고 교착 상태를 일으킬 수 있습니다.  
  
 트랜잭션을 하나의 일괄 처리로 유지하면 트랜잭션 중 네트워크 왕복이 최소화되므로 트랜잭션을 완료하고 잠금을 해제하는 데 걸리는 지연 시간을 줄일 수 있습니다.  
  
#### <a name="use-a-lower-isolation-level"></a>낮은 격리 수준을 사용합니다.  
 트랜잭션을 더 낮은 격리 수준에서 실행할 수 있는지 확인합니다. 커밋된 읽기를 구현하면 트랜잭션에서는 처음 트랜잭션이 완료될 때까지 기다리지 않고 다른 트랜잭션에서 이전에 읽은 수정되지 않은 데이터를 읽을 수 있습니다. 커밋된 읽기 등 낮은 격리 수준을 사용하면 순차 가능 등의 높은 격리 수준보다 짧은 기간 동안 공유 잠금을 보유합니다. 그 결과 잠금 경합이 줄어듭니다.  
  
#### <a name="use-a-row-versioning-based-isolation-level"></a>행 버전 관리 기반의 격리 수준 사용  
 `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 ON으로 설정하면 커밋된 읽기 격리 수준에서 실행되는 트랜잭션은 읽기 작업 동안 공유 잠금 대신 행 버전 관리를 사용합니다.  
  
> [!NOTE]  
> 일부 애플리케이션은 커밋된 읽기 격리의 잠금과 차단에 의존합니다. 이러한 애플리케이션의 경우 이 옵션을 설정하기 전에 몇 가지 사항을 변경해야 합니다.  
  
 스냅샷 격리에서도 읽기 작업 중 공유 잠금을 사용하지 않는 행 버전 관리를 사용합니다. 스냅샷 격리 상태에서 트랜잭션을 실행하려면 먼저 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정해야 합니다.  
  
 읽기 작업과 쓰기 작업 간에 발생할 수 있는 교착 상태를 최소화하려면 이러한 격리 수준을 구현합니다.  
  
#### <a name="use-bound-connections"></a>바인딩된 연결을 사용합니다.  
 바인딩된 연결을 사용하면 같은 애플리케이션에서 열어 놓은 둘 이상의 연결을 함께 사용할 수 있습니다. 보조 연결에서 얻은 잠금은 기본 연결에서 얻은 것과 같이 유지되며 반대의 경우도 마찬가지입니다. 따라서 서로를 차단하지 않습니다.  
  
## <a name="lock-partitioning"></a><a name="lock_partitioning"></a> 잠금 분할  
 잠금을 확보하고 해제하는 과정에서는 내부 잠금 리소스에 대한 경합이 발생하기 때문에 대규모 컴퓨터 시스템의 경우 자주 참조되는 개체를 잠그면 성능이 저하될 수 있습니다. 잠금 분할은 하나의 잠금 리소스를 여러 잠금 리소스로 분할하여 잠금 성능을 높입니다. 이 기능은 CPU가 16개 이상인 시스템에서만 사용할 수 있고 자동으로 설정되며 해제할 수는 없습니다. 개체 잠금만 분할할 수 있습니다. 하위 유형이 있는 개체 잠금은 분할할 수 없습니다. 자세한 내용은 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)를 참조하세요.  
  
### <a name="understanding-lock-partitioning"></a>잠금 분할 이해  
 잠금 태스크에서는 몇 가지 공유 리소스에 액세스하게 되며 잠금 분할을 통해 이 중 두 가지 리소스에 대한 액세스를 최적화할 수 있습니다.  
  
-   **Spinlock**. 행 또는 테이블과 같은 잠금 리소스에 대한 액세스를 제어합니다.  
  
     잠금 분할을 사용하지 않으면 하나의 spinlock이 단일 잠금 리소스에 대한 모든 잠금 요청을 관리하게 됩니다. 작업량이 많은 시스템에서는 여러 잠금 요청이 spinlock을 사용하기 위해 대기하므로 경합이 발생할 수 있습니다. 이러한 상황에서 잠금을 획득하게 되면 병목이 발생하여 성능을 저하시킬 수 있습니다.  
  
     잠금 분할은 단일 잠금 리소스를 여러 잠금 리소스로 분할하여 여러 spinlock에 로드를 분산함으로써 단일 잠금 리소스에 대한 경합을 줄입니다.  
  
-   **메모리**. 잠금 리소스 구조를 저장하는 데 사용됩니다.  
  
     spinlock이 확보되면 잠금 구조가 메모리에 저장된 다음 액세스되고 경우에 따라 수정됩니다. 잠금 액세스를 여러 리소스로 분산하면 CPU 간에 메모리 블록을 전송할 필요가 없으므로 성능이 향상됩니다.  
  
### <a name="implementing-and-monitoring-lock-partitioning"></a>잠금 분할 구현 및 모니터링  
 CPU가 16개 이상인 시스템의 경우 잠금 분할이 기본적으로 설정됩니다. 잠금 분할을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 오류 로그에 정보 메시지가 기록됩니다.  
  
 분할된 리소스에 대해 잠금을 확보하는 경우  
  
-   NL, SCH-S, IS, IU 및 IX 잠금 모드만 단일 파티션에 대해 확보됩니다.  
  
-   NL, SCH-S, IS, IU 및 IX 이외의 모드에서 공유 잠금(S), 배타적 잠금(X) 등의 잠금은 파티션 ID가 0으로 시작하고 파티션 ID 순서를 따르는 모든 파티션에 대해 확보되어야 합니다. 각 파티션은 효율적인 별도의 잠금이 되므로 분할된 리소스에 이러한 대한 잠금은 동일한 모드에서 분할되지 않은 리소스에 대한 잠금보다 메모리를 더 많이 사용합니다. 메모리 증가는 파티션의 수에 따라 결정됩니다. Windows 성능 모니터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 잠금 카운터에는 분할된 잠금과 분할되지 않은 잠금에 사용되는 메모리에 대한 정보가 표시됩니다.  
  
 트랜잭션이 시작되면 파티션에 트랜잭션이 할당됩니다. 트랜잭션의 경우 분할할 수 있는 모든 잠금 요청에는 트랜잭션에 할당된 파티션이 사용됩니다. 이러한 방법으로 동일한 개체의 잠금 리소스에 대한 여러 트랜잭션의 액세스가 여러 파티션으로 분산됩니다.  
  
 `sys.dm_tran_locks` 동적 관리 뷰의 `resource_lock_partition` 열은 잠금 분할 리소스에 대한 잠금 파티션 ID를 제공합니다. 자세한 내용은 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)를 참조하세요.  
  
### <a name="working-with-lock-partitioning"></a>잠금 분할 작업  
 다음은 잠금 분할을 보여 주는 코드 예제입니다. 이 예제에서는 서로 다른 두 세션에서 실행되는 두 가지 트랜잭션을 통해 CPU가 16개인 시스템의 잠금 분할 동작을 보여 줍니다.  
  
 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 이후에 나오는 예제에서 사용되는 테스트 개체를 만듭니다.  
  
```sql  
-- Create a test table.  
CREATE TABLE TestTable  (col1 int);  
GO  
  
-- Create a clustered index on the table.  
CREATE CLUSTERED INDEX ci_TestTable   
    ON TestTable (col1);  
GO  
  
-- Populate the table.  
INSERT INTO TestTable VALUES (1);  
GO  
```  
  
#### <a name="example-a"></a>예 1  
 세션 1:  
  
 트랜잭션에서 `SELECT` 문이 실행됩니다. `HOLDLOCK` 잠금 힌트로 인해 이 문은 해당 테이블에 대해 IS(내재된 공유) 잠금을 획득하여 유지합니다. 이 그림에서는 행 잠금 및 페이지 잠금이 무시됩니다. IS 잠금은 트랜잭션에 할당된 파티션에 대해서만 획득할 수 있습니다. 이 예에서는 파티션 ID 7에 대해 IS 잠금을 획득했다고 가정합니다.  
  
```sql  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
    FROM TestTable  
    WITH (HOLDLOCK);  
```  
  
 세션 2:  
  
 트랜잭션이 시작되고 이 트랜잭션에서 실행되는 `SELECT` 문이 테이블에 대한 S(공유) 잠금을 획득 및 유지합니다. S 잠금은 모든 파티션에 대해 확보되므로 각 파티션에 대해 하나씩 잠금이 생성되어 여러 테이블이 잠기게 됩니다. 예를 들어 CPU가 16개인 시스템에서 잠금 파티션 ID 0-15까지 16개의 잠금이 생성됩니다. S 잠금은 세션 1의 트랜잭션에 의해 파티션 ID 7에 확보된 IS 잠금과 호환되므로 트랜잭션 간에 차단이 발생하지 않습니다.  
  
```sql  
BEGIN TRANSACTION  
    SELECT col1  
    FROM TestTable  
    WITH (TABLOCK, HOLDLOCK);  
```  
  
 세션 1:  
  
 세션 1에서 아직 활성화되어 있는 트랜잭션에서 다음 `SELECT` 문이 실행됩니다. X(배타적) 테이블 잠금 힌트로 인해 트랜잭션이 테이블에 대해 X 잠금을 획득하려 합니다. 그러나 세션 2의 트랜잭션에 의해 확보된 S 잠금이 파티션 ID 0에서 X 잠금을 차단합니다.  
  
```sql  
SELECT col1  
FROM TestTable  
WITH (TABLOCKX);  
```  
  
#### <a name="example-b"></a>예 2  
 세션 1:  
  
 트랜잭션에서 `SELECT` 문이 실행됩니다. `HOLDLOCK` 잠금 힌트로 인해 이 문은 해당 테이블에 대해 IS(내재된 공유) 잠금을 획득하여 유지합니다. 이 그림에서는 행 잠금 및 페이지 잠금이 무시됩니다. IS 잠금은 트랜잭션에 할당된 파티션에 대해서만 획득할 수 있습니다. 이 예에서는 파티션 ID 6에 대해 IS 잠금을 획득했다고 가정합니다.  
  
```sql  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
    FROM TestTable  
    WITH (HOLDLOCK);  
```  
  
 세션 2:  
  
 트랜잭션에서 `SELECT` 문이 실행됩니다. `TABLOCKX` 잠금 힌트로 인해 트랜잭션이 테이블에 대해 X(배타적) 잠금을 획득하려 합니다. 파티션 ID가 0으로 시작하는 모든 파티션에 대해 획득되어야 하므로 X 잠금은 0-5의 모든 파티션 ID에 대해 획득되지만 파티션 ID 6에 획득된 IS 잠금에 의해 차단됩니다.  
  
 아직 X 잠금이 획득되지 않은 파티션 ID 7-15에서 다른 트랜잭션이 계속 잠금을 획득할 수 있습니다.  
  
```sql  
BEGIN TRANSACTION  
    SELECT col1  
    FROM TestTable  
    WITH (TABLOCKX, HOLDLOCK);  
```   
  
##  <a name="row-versioning-based-isolation-levels-in-the-ssdenoversion"></a><a name="Row_versioning"></a>[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 행 버전 관리 기반 격리 수준 사용.  
 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 기존 격리 수준을 구현한 커밋된 읽기를 제공하여 행 버전 관리를 사용하는 문 수준 스냅샷을 제공합니다. 또한 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 트랜잭션 격리 수준인 스냅샷이 도입되어 행 버전 관리를 사용하는 트랜잭션 수준 스냅샷을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 행 버전 관리는 행을 수정하거나 삭제할 때 쓰기 시 복사 메커니즘을 호출하는 일반적인 방법입니다. 이렇게 하려면 트랜잭션을 실행하는 동안 트랜잭션의 일관성 있는 이전 상태가 요구되는 트랜잭션에서 이전 기존 행 버전을 사용할 수 있어야 합니다. 행 버전 관리는 다음 용도로 사용됩니다.  
  
-   트리거에 **inserted** 및 **deleted** 테이블 작성. 트리거에 의해 수정된 모든 행의 버전이 지정됩니다. 여기에는 트리거를 실행한 문에 의해 수정된 행과 트리거에 의해 수정된 모든 데이터가 포함됩니다.  
-   MARS(Multiple Active Result Sets) 지원. 활성 결과 집합이 있을 때 MARS 세션에서 `INSERT`, `UPDATE` 또는 `DELETE`와 같은 데이터 수정 문을 실행하면 이 수정 문의 영향을 받는 행의 버전이 지정됩니다.  
-   ONLINE 옵션을 지정하는 인덱스 작업 지원  
-   행 버전 관리 기반 트랜잭션 격리 수준 지원  
    -   행 버전 관리를 사용하여 문 수준의 읽기 일관성을 유지하는 새로운 커밋된 읽기 격리 수준 구현  
    -   트랜잭션 수준의 읽기 일관성을 유지하는 새로운 스냅샷 격리 수준  
  
 `tempdb` 데이터베이스에는 버전 저장소로 사용할 공간이 충분해야 합니다. `tempdb`이 꽉 차면 업데이트 작업이 버전 생성을 중단하고 계속 진행되지만 필요한 특정 행 버전이 더 이상 존재하지 않으므로 읽기 작업이 실패할 수 있습니다. 이것은 트리거, MARS 및 온라인 인덱싱 등의 작업에 영향을 줍니다.  
  
 커밋된 읽기 및 스냅샷 트랜잭션에 행 버전 관리를 사용하는 과정은 다음 두 단계로 이루어집니다.  
  
1.  `READ_COMMITTED_SNAPSHOT`과 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션 중 하나 또는 모두를 ON에 설정합니다.  
2.  애플리케이션에서 적절한 트랜잭션 격리 수준을 설정합니다.  

    -   `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 ON으로 설정하면 커밋된 읽기 격리 수준을 설정하는 트랜잭션에 행 버전 관리가 사용됩니다.  
    -   `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정하면 트랜잭션에서 스냅샷 격리 수준을 설정할 수 있습니다.  
  
 `READ_COMMITTED_SNAPSHOT` 또는 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 행 버전 관리를 사용하여 데이터를 조작하는 각 트랜잭션에 XSN(트랜잭션 시퀀스 번호)을 할당합니다. 트랜잭션은 `BEGIN TRANSACTION` 문이 실행될 때 시작합니다. 그러나 트랜잭션 시퀀스 번호는 BEGIN TRANSACTION 문 이후 첫 번째 읽기 또는 쓰기 작업이 실행될 때 시작합니다. 트랜잭션 시퀀스 번호는 할당될 때마다 1씩 증가합니다.  
  
 `READ_COMMITTED_SNAPSHOT` 또는 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정하면 데이터베이스에서 수행된 모든 데이터 수정 내용에 대한 논리적 복사본(버전)이 유지됩니다. 특정 트랜잭션에 의해 행이 수정될 때마다 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스는 행의 이전에 커밋된 이미지 버전을 `tempdb`에 저장합니다. 각 버전은 행을 변경한 트랜잭션의 트랜잭션 시퀀스 번호로 표시됩니다. 수정된 행의 여러 버전은 연결 목록을 통해 체인으로 연결됩니다. 최신 행 값은 항상 현재 데이터베이스에 저장되고 `tempdb`에 저장된 버전 지정된 행과 체인으로 연결되어 있습니다.  
  
> [!NOTE]  
> LOB(Large Object) 수정 내용의 경우 변경된 조각만 `tempdb`의 버전 저장소에 복사됩니다.  
  
 행 버전은 행 버전 관리 기반 격리 수준으로 실행되는 트랜잭션의 요구 사항을 만족할 때까지 유지됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 가장 오래된 유용한 트랜잭션 시퀀스 번호를 추적하여 해당 번호보다 낮은 트랜잭션 시퀀스 번호로 표시된 모든 행 버전을 주기적으로 삭제합니다.  
  
 두 가지 데이터베이스 옵션을 모두 OFF로 설정하면 트리거 또는 MARS 세션에 의해 수정되었거나 ONLINE 인덱스 작업에서 읽은 행에만 버전이 지정됩니다. 이러한 행 버전은 더 이상 필요하지 않을 경우 해제됩니다. 백그라운드 스레드가 주기적으로 실행되어 오래되어 필요 없는 행 버전을 제거합니다.  
  
> [!NOTE]  
> 짧게 실행되는 트랜잭션의 경우 수정된 행의 버전이 `tempdb` 데이터베이스의 디스크 파일에 작성되지 않고 버퍼 풀에 캐시될 수 있습니다. 버전이 지정된 행이 일시적으로 필요한 경우에는 버퍼 풀에서 삭제되며 이것이 반드시 I/O 오버헤드를 유발하는 것은 아닐 수도 있습니다.  
  
### <a name="behavior-when-reading-data"></a>데이터를 읽는 경우의 동작  
 행 버전 관리 기반 격리 데이터 읽기 수준으로 트랜잭션이 실행되는 경우에는 읽기 작업에서 읽고 있는 데이터에 대한 공유(S) 잠금을 획득하지 못하므로 데이터를 수정하는 트랜잭션을 차단하지 못합니다. 또한 획득한 잠금 수가 감소함에 따라 리소스 잠금으로 인한 오버헤드가 최소화됩니다. 행 버전 관리를 사용하는 커밋된 읽기 격리 및 스냅샷 격리는 버전이 지정된 데이터에 대해 문 수준 또는 트랜잭션 수준의 읽기 일관성을 유지하도록 디자인되었습니다.  
  
 행 버전 관리 기반 격리 수준에서 실행되는 트랜잭션을 포함하여 모든 쿼리는 컴파일 및 실행 중에 Sch-S(스키마 안정성) 잠금을 획득합니다. 이 때문에 동시 트랜잭션이 테이블에 대해 Sch-M(스키마 수정) 잠금을 유지하면 쿼리가 차단됩니다. 예를 들어 DDL(데이터 정의 언어) 작업은 테이블의 스키마 정보를 수정하기 전에 Sch-M 잠금을 획득합니다. 행 버전 관리 기반 격리 수준에서 실행되는 쿼리 트랜잭션을 포함하여 Sch-S 잠금을 획득하려고 시도하는 쿼리 트랜잭션은 차단됩니다. 반대로 Sch-S 잠금을 유지하는 쿼리는 Sch-M 잠금을 획득하려고 시도하는 동시 트랜잭션을 차단합니다.  
  
 스냅샷 격리 수준을 사용하는 트랜잭션이 시작되면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에서 현재 활성화된 모든 트랜잭션을 기록합니다. 스냅샷 트랜잭션에서 버전 체인이 있는 행을 읽으면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]이 체인을 추적하여 다음과 같은 트랜잭션 시퀀스 번호가 있는 행을 검색합니다.  
  
-   행을 읽는 스냅샷 트랜잭션의 시퀀스 번호보다 낮으면서 가장 근사한 번호  
  
-   스냅샷 트랜잭션이 시작되었을 때 활성화된 트랜잭션의 목록에 없는 번호  
  
 스냅샷 트랜잭션에 따라 수행된 읽기 작업에서는 스냅샷 트랜잭션이 시작되었을 때 커밋된 각 행의 마지막 버전을 검색합니다. 따라서 트랜잭션의 시작 부분에 데이터가 위치하게 되므로 데이터의 스냅샷 트랜잭션이 일관되게 유지됩니다.  
  
 행 버전 관리가 사용된 커밋된 읽기 트랜잭션도 이와 비슷한 방식으로 작동합니다. 다만 커밋된 읽기 트랜잭션에서는 행 버전을 선택할 때 고유한 트랜잭션 시퀀스 번호가 사용되지 않는다는 점이 다릅니다. 문이 시작될 때마다 커밋된 읽기 트랜잭션에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에 대해 생성된 가장 최근의 트랜잭션 시퀀스 번호를 읽습니다. 이 트랜잭션 시퀀스 번호는 해당 문에 대해 올바른 행 버전을 선택하는 데 사용됩니다. 이러한 방법으로 커밋된 읽기 트랜잭션에서 각 문의 시작 부분에 있는 데이터의 스냅샷을 확인할 수 있습니다.  
  
> [!NOTE]  
> 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션은 문 수준에서 트랜잭션이 일관된 데이터 뷰를 제공하지만 이 유형의 트랜잭션에서 생성하거나 액세스한 행 버전은 해당 트랜잭션이 완료될 때까지 유지됩니다.  
  
### <a name="behavior-when-modifying-data"></a>데이터를 수정하는 경우의 동작  
 행 버전 관리가 사용되는 커밋된 읽기 트랜잭션에서는 데이터 값을 읽을 때 데이터 행에 업데이트(U) 잠금이 적용되는 차단 검색을 사용하여 업데이트할 행을 선택합니다. 이것은 행 버전 관리를 사용하지 않는 커밋된 읽기 트랜잭션과 동일합니다. 데이터 행이 업데이트 조건에 맞지 않으면 해당 행의 업데이트 잠금이 해제되고 그 다음 행이 잠겨 검색됩니다.  
  
 스냅샷 격리 수준으로 실행되는 트랜잭션은 제약 조건을 적용하기 위해 수정 내용을 수행하기 전에 데이터에 대한 잠금을 획득하는 낙관적 데이터 수정 방법을 사용합니다. 그렇지 않으면 데이터가 수정될 때까지 데이터에 대한 잠금도 획득되지 않습니다. 스냅샷 트랜잭션은 데이터 행이 업데이트 조건에 맞으면 이 스냅샷 트랜잭션이 시작된 후 커밋된 동시 트랜잭션에 의해 해당 데이터 행이 수정되지 않았는지 확인합니다. 스냅샷 트랜잭션이 아닌 다른 트랜잭션에 의해 데이터 행이 수정된 경우에는 업데이트 충돌이 발생하고 스냅샷 트랜잭션이 종료됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 업데이트 충돌을 처리합니다. 업데이트 충돌 검색 기능은 해제할 수 없습니다.  
  
> [!NOTE]  
> 내부적으로 스냅샷 격리 수준으로 실행되는 업데이트 작업은 스냅샷 트랜잭션이 다음 항목에 액세스할 때는 커밋된 읽기 격리 수준으로 실행됩니다.  
>  
> FOREIGN KEY 제약 조건이 있는 테이블  
>  
> 다른 테이블의 FOREIGN KEY 제약 조건에서 참조되는 테이블  
>  
> 둘 이상의 테이블을 참조하는 인덱싱된 뷰  
>  
> 그러나 이러한 조건에서도 업데이트 작업은 다른 트랜잭션에 의해 데이터가 수정되지 않았는지 확인합니다. 다른 트랜잭션에 의해 데이터가 수정된 경우 스냅샷 트랜잭션에서 업데이트 충돌이 발생하고 종료됩니다.  
  
### <a name="behavior-in-summary"></a>동작 요약  
 다음 표에서는 행 버전 관리를 사용하는 스냅샷 격리와 커밋된 읽기 격리의 차이점을 요약합니다.  
  
|속성|행 버전 관리를 사용하는 커밋된 읽기 격리 수준|스냅샷 격리 수준|  
|--------------|----------------------------------------------------------|------------------------------|  
|지원 요구 사항에 따라 ON으로 설정되어야 하는 데이터베이스 옵션|READ_COMMITTED_SNAPSHOT|ALLOW_SNAPSHOT_ISOLATION|  
|세션에서 특정한 유형의 행 버전 관리를 요청하는 방법|기본 커밋된 읽기 격리 수준을 사용하거나 SET TRANSACTION ISOLATION LEVEL 문을 실행하여 READ COMMITTED 격리 수준을 지정합니다. 이 작업은 트랜잭션이 시작된 후에 수행할 수 있습니다.|트랜잭션이 시작되기 전에 SET TRANSACTION ISOLATION LEVEL 문을 실행하여 SNAPSHOT 격리 수준을 지정해야 합니다.|  
|문에서 읽는 데이터의 버전|각 문이 시작되기 전에 커밋된 모든 데이터|각 트랜잭션이 시작되기 전에 커밋된 모든 데이터|  
|업데이트 처리 방법|행 버전을 실제 데이터로 변환하여 업데이트할 행을 선택하고 선택한 데이터 행에 업데이트 잠금을 사용합니다. 수정할 실제 데이터 행에 대해 배타적 잠금을 획득합니다. 업데이트 충돌 검색은 사용되지 않습니다.|행 버전을 사용하여 업데이트할 행을 선택합니다. 수정할 실제 데이터 행에 대해 배타적 잠금을 획득하려고 시도합니다. 데이터가 다른 트랜잭션에 의해 이미 수정된 경우에는 업데이트 충돌이 발생하며 스냅샷 트랜잭션이 종료됩니다.|  
|업데이트 충돌 검색|없음|통합 지원되며 해제할 수 없습니다.|  
  
### <a name="row-versioning-resource-usage"></a>행 버전 관리 리소스 사용  
 행 버전 관리 프레임워크는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 다음 기능을 지원합니다.  
  
-   트리거  
-   MARS(Multiple Active Results Sets)  
-   온라인 인덱싱  
  
 또한 행 버전 관리 프레임워크는 다음 행 버전 관리 기반 트랜잭션 격리 수준을 지원합니다. 이러한 격리 수준은 기본적으로 설정되지 않습니다.  
  
-   `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션이 ON이면 `READ_COMMITTED` 트랜잭션이 행 버전 관리를 사용하여 문 수준의 읽기 일관성을 제공합니다.  
-   `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션이 ON이면 `SNAPSHOT` 트랜잭션이 행 버전 관리를 사용하여 트랜잭션 수준의 읽기 일관성을 제공합니다.  
  
 행 버전 관리 기반 격리 수준을 이용하면 읽기 작업에 대해 공유 잠금을 사용하지 않아도 되므로 트랜잭션에 의해 확보되는 잠금 수가 줄어듭니다. 결과적으로 잠금 관리에 사용되는 리소스가 줄어 시스템 성능이 향상됩니다. 또한 다른 트랜잭션에 의해 확보된 잠금으로 인해 트랜잭션이 차단되는 횟수도 줄어 성능이 한층 더 향상됩니다.  
  
 행 버전 관리 기반 격리 수준을 이용하면 데이터 수정에 필요한 리소스가 늘어납니다. 이 옵션을 설정하면 데이터베이스의 모든 데이터 수정에 대해 버전이 지정됩니다. 행 버전 관리 기반 격리를 사용하는 활성 트랜잭션이 없는 경우에도 수정 전에 데이터의 복사본이 tempdb에 저장됩니다. 수정 후의 데이터에는 tempdb에 저장된 버전 지정 데이터에 대한 포인터가 포함됩니다. 큰 개체의 경우 개체의 변경된 부분만 tempdb에 복사됩니다.  
  
#### <a name="space-used-in-tempdb"></a>TempDB의 사용된 공간  
 각 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스의 tempdb에는 해당 인스턴스의 모든 데이터베이스에 대해 생성된 행 버전을 보유할 수 있는 공간이 있어야 합니다. 데이터베이스 관리자는 TempDB에 버전 저장소를 포함할 수 있는 충분한 공간이 있는지를 확인해야 합니다. TempDB에는 다음의 두 버전 저장소가 있습니다.  
  
-   온라인 인덱스 작성 버전 저장소는 모든 데이터베이스의 온라인 인덱스 작성에 사용됩니다.  
-   공용 버전 저장소는 모든 데이터베이스의 다른 모든 데이터 수정 작업에 사용됩니다.  
  
 활성 트랜잭션에서 행 버전에 액세스해야 하는 동안에는 행 버전이 저장되어야 합니다. 1분마다 백그라운드 스레드가 필요 없게 된 행 버전을 제거하여 TempDB에서 공간을 비웁니다. 다음 중 하나에 해당될 경우 장기 실행 트랜잭션은 버전 저장소의 공간이 해제되지 않도록 합니다.  
  
-   행 버전 관리 기반 격리를 사용합니다.  
-   트리거, MARS 또는 온라인 인덱스 작성 작업을 사용합니다.  
-   행 버전을 생성합니다.  
  
> [!NOTE]  
> 트랜잭션 내부에서 트리거를 호출하면 해당 트리거에 의해 생성된 행 버전은 트리거가 완료된 후 행 버전이 더 이상 필요하지 않아도 트랜잭션이 끝날 때까지 유지됩니다. 이는 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션에도 적용됩니다. 이 유형의 트랜잭션에서는 트랜잭션의 각 문에 대해서만 데이터베이스의 트랜잭션 뷰가 일치해야 하므로 문이 완료된 후에는 트랜잭션의 문에 대해 생성된 행 버전이 필요하지 않습니다. 그러나 트랜잭션의 각 문에 의해 생성된 행 버전은 트랜잭션이 완료될 때까지 유지됩니다.  
  
 TempDB의 공간이 부족하면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 버전 저장소를 강제로 축소합니다. 축소하는 동안, 아직 행 버전을 생성하지 않은 트랜잭션 중 장기 실행 트랜잭션은 교착 상태가 발생한 것으로 표시됩니다. 오류 로그에는 교착 상태가 발생한 각 트랜잭션에 대해 메시지 3967이 생성됩니다. 교착 상태가 발생한 것으로 표시된 트랜잭션은 버전 저장소의 행 버전을 더 이상 읽을 수 없습니다. 행 버전을 읽으려고 하면 메시지 3966이 생성되고 트랜잭션이 롤백됩니다. 축소하는 데 성공하면 tempdb에서 공간을 사용할 수 있게 됩니다. 그렇지 않으면 tempdb의 공간이 부족해지고 다음과 같은 상황이 발생합니다.  
  
-   쓰기 작업이 계속 실행되지만 버전을 생성하지 않습니다. 오류 로그에 정보 메시지(3959)가 나타납니다. 데이터를 기록한 트랜잭션은 영향을 받지 않습니다.  
  
-   tempdb의 완전 롤백으로 인해 생성되지 않은 행 버전에 액세스하려고 하는 트랜잭션은 오류 3958과 함께 종료됩니다.  
  
#### <a name="space-used-in-data-rows"></a>데이터 행의 공간 사용량  
 각 데이터베이스 행의 행 끝에서 최대 14바이트를 사용하여 행 버전 관리 정보를 저장할 수 있습니다. 행 버전 관리 정보에는 버전을 커밋한 트랜잭션의 트랜잭션 시퀀스 번호와 버전이 지정된 행에 대한 포인터가 포함됩니다. 이 14바이트는 다음과 같은 조건에서 행이 처음 수정될 때 또는 새 행이 삽입될 때 추가됩니다.  
  
-   `READ_COMMITTED_SNAPSHOT` 또는 `ALLOW_SNAPSHOT_ISOLATION` 옵션은 ON입니다.  
-   테이블에 트리거가 있습니다.  
-   MARS(Multiple Active Results Sets)를 사용하고 있습니다.  
-   테이블에서 현재 온라인 인덱스 작성 작업이 실행되고 있습니다.  
  
 이 14바이트는 다음과 같은 조건에서 행이 처음 수정될 때 데이터베이스 행에서 제거됩니다.  
  
-   `READ_COMMITTED_SNAPSHOT` 및 `ALLOW_SNAPSHOT_ISOLATION` 옵션은 OFF입니다.  
-   테이블에 트리거가 없습니다.  
-   MARS를 사용하고 있지 않습니다.  
-   현재 온라인 인덱스 작성 작업이 실행되고 있지 않습니다.  
  
 행 버전 관리 기능을 사용하는 경우에는 데이터베이스 행당 14바이트를 사용할 수 있도록 데이터베이스에 더 많은 디스크 공간을 할당해야 할 수 있습니다. 행 버전 관리 정보를 추가하면 인덱스 페이지가 분할되거나 현재 페이지에 사용 가능한 공간이 충분하지 않은 경우에는 새 데이터 페이지가 할당될 수 있습니다. 예를 들어 평균 행 길이가 100바이트인 경우 14바이트를 추가하면 기존 테이블이 최대 14% 증가할 수 있습니다.  
  
 [채우기 비율](../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 낮추면 인덱스 페이지의 조각화를 방지하거나 줄일 수 있습니다. 테이블 또는 뷰의 데이터와 인덱스에 대한 조각화 정보를 보려면 [sys.dm_db_index_physical_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 사용합니다.  
  
#### <a name="space-used-in-large-objects"></a>큰 개체의 공간 사용량  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 최대 2GB의 큰 문자열을 저장할 수 있는 6개의 데이터 형식을 지원합니다. 6개의 데이터 형식은 `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text` 및 `image`입니다. 이러한 데이터 형식을 사용하여 저장된 큰 문자열은 데이터 행에 연결된 일련의 데이터 조각에 저장됩니다. 행 버전 관리 정보는 큰 문자열이 저장된 각 조각에 저장됩니다. 데이터 조각은 테이블의 큰 개체에만 사용되는 페이지의 모음입니다.  
  
 데이터베이스에 새로 큰 값이 추가될 때 조각당 최대 8040바이트의 데이터가 할당됩니다. 이전 버전의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 조각당 최대 8080바이트의 `ntext`, `text` 또는 `image` 데이터를 저장했습니다.  
  
 이전 버전의 `ntext`에서 `text`로 데이터베이스를 업그레이드한 경우에는 행 버전 관리 정보를 저장할 공간을 만들기 위해 기존 `image`, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] LOB(Large Object) 데이터가 업데이트되지 않습니다. 그러나 LOB 데이터가 처음 수정될 때는 버전 관리 정보를 스토리지할 수 있도록 데이터가 동적으로 업그레이드됩니다. 이는 행 버전이 생성되지 않은 경우에도 마찬가지입니다. LOB 데이터가 업그레이드된 후에는 조각당 저장되는 최대 바이트 수가 8080바이트에서 8040바이트로 줄어듭니다. 업그레이드 프로세스에서는 LOB 값을 삭제하고 동일한 값을 다시 삽입합니다. 1바이트만 수정되더라도 LOB 데이터가 업그레이드됩니다. 이 작업은 각 `ntext`, `text` 또는 `image` 열에 대해 한 번 수행되지만 LOB 데이터의 크기에 따라 각 작업 수행 시 대량의 페이지 할당 및 I/O 작업이 발생할 수 있습니다. 수정 내용 전체가 로깅되는 경우에는 대량의 로깅 작업이 발생할 수도 있습니다. 데이터베이스 복구 모드를 FULL로 설정하지 않으면 WRITETEXT와 UPDATETEXT 작업에서 최소한의 정보만 로깅합니다.  
  
 `nvarchar(max)`, `varchar(max)` 및 `varbinary(max)` 데이터 형식은 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 사용할 수 없으므로 업그레이드 문제가 발생하지 않습니다.  
  
 이 요구 사항을 충족하는 충분한 디스크 공간을 할당해야 합니다.  
  
#### <a name="monitoring-row-versioning-and-the-version-store"></a>행 버전 관리 및 버전 저장소 모니터링  
 행 버전 관리, 버전 저장소 및 스냅샷 격리 프로세스의 성능과 문제를 모니터링하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 DMV(동적 관리 뷰) 및 Windows 시스템 모니터의 성능 카운터 형태로 도구를 제공합니다.  
  
##### <a name="dmvs"></a>DMV  
 다음 DMV는 tempdb와 버전 저장소 및 행 버전 관리를 사용하는 트랜잭션의 현재 상태에 대한 정보를 제공합니다.  
  
 sys.dm_db_file_space_usage. 데이터베이스의 각 파일에 대한 공간 사용량 정보를 반환합니다. 자세한 내용은 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)를 참조하세요.  
  
 sys.dm_db_session_space_usage. 데이터베이스에서 발생하는 세션별 페이지 할당 및 할당 취소 작업을 반환합니다. 자세한 내용은 [sys.dm_db_session_space_usage&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)를 참조하세요.  
  
 sys.dm_db_task_space_usage. 데이터베이스에서 발생하는 태스크별로 페이지 할당 및 할당 취소 작업을 반환합니다. 자세한 내용은 [sys.dm_db_task_space_usage&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)를 참조하세요.  
  
 sys.dm_tran_top_version_generators. 버전 저장소의 버전 대부분을 생성하는 개체에 대한 가상 테이블을 반환합니다. 256개의 집계 레코드 길이를 database_id 및 rowset_id에 따라 그룹화합니다. 이 함수를 사용하면 버전 저장소를 가장 많이 사용하는 소비자를 찾을 수 있습니다. 자세한 내용은 [sys.dm_tran_top_version_generators&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-top-version-generators-transact-sql.md)를 참조하세요.  
  
 sys.dm_tran_version_store. 공용 버전 저장소의 모든 버전 레코드를 표시하는 가상 테이블을 반환합니다. 자세한 내용은 [sys.dm_tran_version_store&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)를 참조하세요.  

 sys.dm_tran_version_store_space_usage. 각 데이터베이스에 대한 버전 저장소 레코드에서 사용되는 tempdb의 총 공간을 표시하는 가상 테이블을 반환합니다. 자세한 내용은 [sys.dm_tran_version_store_space_usage&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)를 참조하세요.  

> [!NOTE]  
> sys.dm_tran_top_version_generators와 sys.dm_tran_version_store 함수는 버전 저장소 전체를 쿼리하므로 버전 저장소의 크기가 클 경우에는 실행하는 데 비용이 많이 들 수 있습니다.  
> sys.dm_tran_version_store_space_usage는 개별 버전 저장소 레코드를 탐색하지 않고 데이터베이스 당 tempdb에서 사용되는 집계된 버전 저장소 공간을 반환하므로 실행하기 효율적이고 비용이 많이 들지 않습니다.
  
 sys.dm_tran_active_snapshot_database_transactions. 행 버전 관리를 사용하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 내의 모든 데이터베이스에 있는 전체 활성 트랜잭션에 대한 가상 테이블을 반환합니다. 시스템 트랜잭션은 이 DMV에 나타나지 않습니다. 자세한 내용은 [sys.dm_tran_active_snapshot_database_transactions&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)을 참조하세요.  
  
 sys.dm_tran_transactions_snapshot. 각 트랜잭션에서 사용한 스냅샷을 표시하는 가상 테이블을 반환합니다. 스냅샷에는 행 버전 관리를 사용하는 활성 트랜잭션의 시퀀스 번호가 포함됩니다. 자세한 내용은 [sys.dm_tran_transactions_snapshot&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-transactions-snapshot-transact-sql.md)을 참조하세요.  
  
 sys.dm_tran_current_transaction. 현재 세션에 있는 트랜잭션의 행 버전 관리 관련 상태 정보를 표시하는 단일 행을 반환합니다. 자세한 내용은 [sys.dm_tran_current_transaction&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md)을 참조하세요.  
  
 sys.dm_tran_current_snapshot. 현재 스냅샷 격리 트랜잭션이 시작될 때의 모든 활성 트랜잭션을 표시하는 가상 테이블을 반환합니다. 현재 트랜잭션에서 스냅샷 격리를 사용중인 경우 이 함수는 행을 반환하지 않습니다. sys.dm_tran_current_snapshot이 현재 스냅샷에 대한 활성 트랜잭션만 반환한다는 점을 제외하고 sys.dm_tran_transactions_snapshot과 비슷합니다. 자세한 내용은 [sys.dm_tran_current_snapshot&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-snapshot-transact-sql.md)을 참조하세요.  
  
##### <a name="performance-counters"></a>성능 카운터  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 성능 카운터는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로세스의 영향을 받는 시스템 성능에 대한 정보를 제공합니다. 다음 성능 카운터는 tempdb와 버전 저장소 및 행 버전 관리를 사용하는 트랜잭션을 모니터링합니다. 이러한 성능 카운터는 SQLServer:Transactions 성능 개체에 포함되어 있습니다.  
  
 **Free Space in tempdb (KB)** . tempdb 데이터베이스의 사용 가능한 공간(KB)을 모니터링합니다. tempdb에는 스냅샷 격리를 지원하는 버전 저장소를 처리하기에 충분한 공간이 있어야 합니다.  
  
 다음 공식을 사용하여 버전 저장소의 예상 크기를 대략적으로 계산할 수 있습니다. 장기 실행 트랜잭션의 경우 생성 및 정리 속도를 모니터링하여 버전 저장소의 예상 최대 크기를 결정하면 유용합니다.  
  
 [공용 버전 저장소의 크기] = 2 * [분당 생성되는 버전 저장소 데이터] \* [트랜잭션의 최장 실행 시간(분)]  
  
 트랜잭션의 최장 실행 시간에는 온라인 인덱스 작성이 포함되지 않습니다. 큰 테이블의 경우 온라인 인덱스 작성 작업에 많은 시간이 소요되므로 이 작업은 별도의 버전 저장소를 사용합니다. 온라인 인덱스 작성 버전 저장소의 크기는 온라인 인덱스 작성을 수행하는 동안 모든 인덱스를 포함하여 테이블에서 수정된 전체 데이터 양과 거의 같습니다.  
  
 **Version Store Size (KB)** . 모든 버전 저장소의 크기(KB)를 모니터링합니다. 이 정보를 통해 tempdb 데이터베이스의 버전 저장소에 필요한 공간을 결정할 수 있습니다. 이 카운터를 지속적으로 모니터링하면 tempdb에 필요한 추가 공간을 예측할 수 있습니다.  
  
 `Version Generation rate (KB/s)`. 모든 버전 저장소의 버전 생성 속도(KB/초)를 모니터링합니다.  
  
 `Version Cleanup rate (KB/s)`. 모든 버전 저장소의 버전 정리 속도(KB/초)를 모니터링합니다.  
  
> [!NOTE]  
> Version Generation rate (KB/s) 및 Version Cleanup rate (KB/s)에서 제공하는 정보를 통해 tempdb에 필요한 공간을 예측할 수 있습니다.  
  
 **Version Store unit count**. 버전 저장소 단위 수를 모니터링합니다.  
  
 **Version Store unit creation**. 인스턴스가 시작된 이후 행 버전을 저장하기 위해 생성된 버전 저장소 단위의 총 수를 모니터링합니다.  
  
 **Version Store unit truncation**. 인스턴스가 시작된 이후 잘린 버전 저장소 단위의 총 수를 모니터링합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 버전 저장소 단위에 저장된 버전 행이 활성 트랜잭션을 실행하는 데 불필요하다고 결정하면 버전 저장소 단위가 잘립니다.  
  
 **Update conflict ratio**. 총 업데이트 스냅샷 트랜잭션 중 업데이트 충돌이 있는 업데이트 스냅샷 트랜잭션의 비율을 모니터링합니다.  
  
 **Longest Transaction Running Time**. 행 버전 관리를 사용하는 트랜잭션의 가장 긴 실행 시간(초)을 모니터링합니다. 이 정보를 사용하면 특별한 이유 없이 오래 실행되는 트랜잭션이 있는지를 확인할 수 있습니다.  
  
 **트랜잭션**. 활성 트랜잭션의 총 수를 모니터링합니다. 시스템 트랜잭션은 포함되지 않습니다.  
  
 `Snapshot Transactions`. 활성 스냅샷 트랜잭션의 총 수를 모니터링합니다.  
  
 `Update Snapshot Transactions`. 업데이트 작업을 수행하는 활성 스냅샷 트랜잭션의 총 수를 모니터링합니다.  
  
 `NonSnapshot Version Transactions`. 버전 레코드를 생성하는 활성 비스냅샷 트랜잭션의 총 수를 모니터링합니다.  
  
> [!NOTE]  
> Update Snapshot Transactions와 NonSnapshot Version Transactions의 합은 버전 생성에 참여하는 트랜잭션의 총 수를 나타냅니다. Snapshot Transactions와 Update Snapshot Transactions 값의 차이를 보고 읽기 전용 스냅샷 트랜잭션의 수를 알 수 있습니다.  
  
### <a name="row-versioning-based-isolation-level-example"></a>행 버전 관리 기반 격리 수준 예  
 다음 예에서는 스냅샷 격리 트랜잭션과 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 동작의 차이를 보여 줍니다.  
  
#### <a name="a-working-with-snapshot-isolation"></a>A. 스냅샷 격리 작업  
 이 예에서는 스냅샷 격리에서 실행되는 트랜잭션이 다른 트랜잭션에서 수정한 데이터를 읽습니다. 스냅샷 트랜잭션은 다른 트랜잭션에서 실행하는 업데이트 작업을 차단하지 않으며 데이터 수정을 무시하고 계속 버전이 지정된 행에서 데이터를 읽습니다. 그러나 스냅샷 트랜잭션이 다른 트랜잭션에서 이미 수정한 데이터를 수정할 경우 스냅샷 트랜잭션은 오류를 생성하고 종료됩니다.  
  
 세션 1:  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Enable snapshot isolation on the database.  
ALTER DATABASE AdventureWorks2016  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Start a snapshot transaction  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 2:  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under snapshot isolation shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 1:  
  
```sql  
    -- Reissue the SELECT statement - this shows  
    -- the employee having 48 vacation hours.  The  
    -- snapshot transaction is still reading data from  
    -- the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 2:  
  
```sql  
-- Commit the transaction; this commits the data  
-- modification.  
COMMIT TRANSACTION;  
GO  
```  
  
 세션 1:  
  
```sql  
    -- Reissue the SELECT statement - this still   
    -- shows the employee having 48 vacation hours  
    -- even after the other transaction has committed  
    -- the data modification.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- Because the data has been modified outside of the  
    -- snapshot transaction, any further data changes to   
    -- that data by the snapshot transaction will cause   
    -- the snapshot transaction to fail. This statement   
    -- will generate a 3960 error and the transaction will   
    -- terminate.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION  
GO  
```  
  
#### <a name="b-working-with-read-committed-using-row-versioning"></a>B. 행 버전 관리를 사용한 커밋된 읽기 작업  
 이 예에서 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션은 다른 트랜잭션과 동시에 실행됩니다. 커밋된 읽기 트랜잭션은 스냅샷 트랜잭션과 다르게 동작합니다. 스냅샷 트랜잭션과 마찬가지로 커밋된 읽기 트랜잭션도 다른 트랜잭션이 데이터를 수정한 이후에 버전이 지정된 행을 읽습니다. 그러나 커밋된 읽기 트랜잭션은 스냅샷 트랜잭션과 달리 다음 작업을 수행합니다.  
  
-   다른 트랜잭션이 데이터 변경 내용을 커밋한 이후에 수정한 데이터를 읽습니다.  
-   스냅샷 트랜잭션과 달리 다른 트랜잭션에서 수정한 데이터를 업데이트할 수 있습니다.  
  
 세션 1:  
  
```sql  
USE AdventureWorks2016;  -- Or any earlier version of the AdventureWorks database.  
GO  
  
-- Enable READ_COMMITTED_SNAPSHOT on the database.  
-- For this statement to succeed, this session  
-- must be the only connection to the AdventureWorks2016  
-- database.  
ALTER DATABASE AdventureWorks2016  
    SET READ_COMMITTED_SNAPSHOT ON;  
GO  
  
-- Start a read-committed transaction  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 2:  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under read-committed using row versioning shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 1:  
  
```sql  
    -- Reissue the SELECT statement - this still shows  
    -- the employee having 48 vacation hours.  The  
    -- read-committed transaction is still reading data   
    -- from the versioned row and the other transaction   
    -- has not committed the data changes yet.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 세션 2:  
  
```sql  
-- Commit the transaction.  
COMMIT TRANSACTION;  
GO  
```  
  
 세션 1:  
  
```sql  
    -- Reissue the SELECT statement which now shows the   
    -- employee having 40 vacation hours.  Being   
    -- read-committed, this transaction is reading the   
    -- committed data. This is different from snapshot  
    -- isolation which reads from the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- This statement, which caused the snapshot transaction   
    -- to fail, will succeed with read-committed using row versioning.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION;  
GO  
```  
  
### <a name="enabling-row-versioning-based-isolation-levels"></a>행 버전 관리 기반 격리 수준 설정  
 데이터베이스 관리자는 ALTER DATABASE 문에서 `READ_COMMITTED_SNAPSHOT` 및 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 사용하여 행 버전 관리에 대한 데이터베이스 수준 설정을 제어합니다.  
  
 `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 ON으로 설정하면 이 옵션을 지원하는 메커니즘이 즉시 활성화됩니다. READ_COMMITTED_SNAPSHOT 옵션을 설정할 때는 `ALTER DATABASE` 명령을 실행하는 연결만 데이터베이스에서 허용됩니다. ALTER DATABASE 명령 실행이 완료될 때까지 데이터베이스에서 다른 열린 연결이 없어야 합니다. 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다.  
  
 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 `READ_COMMITTED_SNAPSHOT`을 활성화합니다.  
  
```sql  
ALTER DATABASE AdventureWorks2016  
    SET READ_COMMITTED_SNAPSHOT ON;  
```  
  
 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정하면 데이터베이스에서 데이터를 수정한 모든 활성 트랜잭션이 완료될 때까지 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스가 수정된 데이터에 대해 행 버전을 생성하지 않습니다. 활성 수정 트랜잭션이 있으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이 옵션의 상태를 `PENDING_ON`로 설정합니다. 모든 수정 트랜잭션이 완료된 후에는 이 옵션의 상태가 ON으로 변경됩니다. 사용자는 이 옵션이 완전히 ON으로 설정되기 전까지는 해당 데이터베이스에서 스냅샷 트랜잭션을 시작할 수 없습니다. 데이터베이스 관리자가 `ALLOW_SNAPSHOT_ISOLATION` 옵션을 OFF로 설정하면 데이터베이스의 상태가 먼저 PENDING_OFF가 된 후 OFF로 변경됩니다.  
  
 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 ALLOW_SNAPSHOT_ISOLATION을 설정합니다.  
  
```sql  
ALTER DATABASE AdventureWorks2016  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
```  
  
 다음 표에서는 ALLOW_SNAPSHOT_ISOLATION 옵션을 나열하고 각각의 상태에 대해 설명합니다. ALTER DATABASE에 ALLOW_SNAPSHOT_ISOLATION 옵션을 사용할 경우 현재 데이터베이스 데이터에 액세스하고 있는 사용자는 차단되지 않습니다.  
  
|현재 데이터베이스에 대한 스냅샷 격리 프레임워크의 상태|Description|  
|----------------------------------------------------------------|-----------------|  
|OFF|스냅샷 격리 트랜잭션에 대한 지원이 활성화되지 않았습니다. 스냅샷 격리 트랜잭션이 허용되지 않습니다.|  
|PENDING_ON|스냅샷 격리 트랜잭션에 대한 지원이 OFF에서 ON으로 전환되는 중입니다. 열린 트랜잭션을 완료해야 합니다.<br /><br /> 스냅샷 격리 트랜잭션이 허용되지 않습니다.|  
|켜기|스냅샷 격리 트랜잭션에 대한 지원이 활성화되었습니다.<br /><br /> 스냅샷 트랜잭션이 허용됩니다.|  
|PENDING_OFF|스냅샷 격리 트랜잭션에 대한 지원이 ON에서 OFF로 전환되는 중입니다.<br /><br /> 이 시점 이후에 시작된 스냅샷 트랜잭션은 이 데이터베이스에 액세스할 수 없습니다. 업데이트 트랜잭션은 이 데이터베이스에서 계속해서 버전 관리를 수행합니다. 기존 스냅샷 트랜잭션은 문제 없이 이 데이터베이스에 액세스할 수 있습니다. 데이터베이스 스냅샷 격리 상태가 ON이었을 때 활성화되어 있던 스냅샷 트랜잭션이 모두 완료되어야 PENDING_OFF 상태가 OFF로 변경됩니다.|  
  
 두 행 버전 관리 데이터베이스 옵션의 상태를 확인하려면 `sys.databases` 카탈로그 뷰를 사용합니다.  
  
 모든 사용자 테이블과 master 및 msdb에 저장된 일부 시스템 테이블에 대한 모든 업데이트는 행 버전을 생성합니다.  
  
 master 및 msdb 데이터베이스에서는 `ALLOW_SNAPSHOT_ISOLATION` 옵션이 자동으로 ON으로 설정되고 비활성화할 수 없습니다.  
  
 사용자는 master, tempdb 또는 msdb에서 `READ_COMMITTED_SNAPSHOT` 옵션을 ON으로 설정할 수 없습니다.  
  
### <a name="using-row-versioning-based-isolation-levels"></a>행 버전 관리 기반 격리 수준 사용  
 행 버전 관리 프레임워크는 항상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 설정되어 있으며 여러 기능에 사용됩니다. 행 버전 관리 기반 격리 수준을 제공할 뿐만 아니라 MARS(Multiple Active Result Set) 세션과 트리거의 수정 내용을 지원하고 온라인 인덱스 작업을 위한 데이터 읽기를 지원하는 데 사용됩니다.  
  
 행 버전 관리 기반 격리 수준은 데이터베이스 수준에서 설정됩니다. 설정된 데이터베이스의 개체에 액세스하는 애플리케이션은 모두 다음과 같은 격리 수준을 사용하여 쿼리를 실행할 수 있습니다.  
  
-   다음 코드 예제에서는 `READ_COMMITTED_SNAPSHOT` 데이터베이스 옵션을 `ON`으로 설정하여 행 버전 관리를 사용하는 커밋된 읽기를 보여 줍니다.  
  
    ```sql  
    ALTER DATABASE AdventureWorks2016  
        SET READ_COMMITTED_SNAPSHOT ON;  
    ```  
  
     데이터베이스에 `READ_COMMITTED_SNAPSHOT`을 설정하면 커밋된 읽기 격리 수준으로 실행되는 모든 쿼리에 행 버전 관리가 사용됩니다. 즉, 읽기 작업 시 업데이트 작업이 차단되지 않습니다.  
  
-   다음 코드 예에서는 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 `ON`으로 설정하여 스냅샷 격리를 보여 줍니다.  
  
    ```sql  
    ALTER DATABASE AdventureWorks2016  
        SET ALLOW_SNAPSHOT_ISOLATION ON;  
    ```  
  
     스냅샷 격리로 실행되는 트랜잭션은 스냅샷이 설정된 데이터베이스의 테이블에 액세스할 수 있습니다. 스냅샷이 설정되지 않은 테이블에 액세스하려면 격리 수준을 변경해야 합니다. 예를 들어 다음 코드 예제에서는 스냅샷 트랜잭션으로 실행되는 동안 두 테이블을 조인하는 `SELECT` 문을 보여 줍니다. 한 테이블은 스냅샷 격리가 설정되지 않은 데이터베이스에 속합니다. 스냅샷 격리에서 `SELECT` 문을 실행하면 실행이 실패합니다.  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
     다음 코드 예제에서는 트랜잭션 격리 수준을 커밋된 읽기로 변경하도록 수정된 동일한 `SELECT` 문을 보여 줍니다. 이렇게 변경하면 `SELECT` 문이 성공적으로 실행됩니다.  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            WITH (READCOMMITTED)  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
#### <a name="limitations-of-transactions-using-row-versioning-based-isolation-levels"></a>행 버전 관리 기반 격리 수준을 사용하는 트랜잭션의 제한 사항  
 행 버전 관리 기반 격리 수준을 사용할 때 다음 제한 사항을 고려하십시오.  
  
-   tempdb, msdb 또는 master에는 `READ_COMMITTED_SNAPSHOT`을 설정할 수 없습니다.  
-   전역 임시 테이블은 tempdb에 저장됩니다. 스냅샷 트랜잭션 내의 전역 임시 테이블에 액세스할 때 다음 중 하나를 수행해야 합니다.  
    -   tempdb에서 `ALLOW_SNAPSHOT_ISOLATION` 데이터베이스 옵션을 ON으로 설정합니다.  
    -   격리 힌트를 사용하여 문에 대한 격리 수준을 변경합니다.  
-   다음과 같은 경우 스냅샷 트랜잭션이 실패합니다.  
    -   스냅샷 트랜잭션이 시작된 후 데이터베이스에 액세스하기 전에 데이터베이스가 읽기 전용으로 설정됩니다.  
    -   여러 데이터베이스의 개체에 액세스하는 경우 스냅샷 트랜잭션이 시작된 후 데이터베이스에 액세스하기 전에 데이터베이스 복구를 수반하는 방식으로 데이터베이스 상태가 변경됩니다. 예를 들어 데이터베이스가 OFFLINE으로 설정되었다가 ONLINE으로 설정되거나 데이터베이스가 자동으로 닫히고 열리거나 데이터베이스가 분리되고 연결됩니다.  
-   분산 분할된 데이터베이스의 쿼리를 포함하여 분산 트랜잭션은 스냅샷 격리로 지원되지 않습니다.  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 여러 버전의 시스템 메타데이터를 보관하지 않습니다. 테이블의 DDL(데이터 정의 언어) 문이나 기타 데이터베이스 개체(인덱스, 뷰, 데이터 형식, 저장 프로시저 및 공용 언어 런타임 함수)는 메타데이터를 변경합니다. DDL 문이 개체를 수정하면 스냅샷 격리의 개체에 대한 동시 참조로 인해 스냅샷 트랜잭션이 실패합니다. READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON이면 커밋된 읽기 트랜잭션에 이러한 제한 사항이 없습니다.  
  
     예를 들어 데이터베이스 관리자가 다음 `ALTER INDEX` 문을 실행합니다.  
  
    ```sql  
    USE AdventureWorks2016;  
    GO  
    ALTER INDEX AK_Employee_LoginID  
        ON HumanResources.Employee REBUILD;  
    GO  
    ```  
  
     `ALTER INDEX` 문이 실행된 후 `HumanResources.Employee` 테이블을 참조하려고 하면 `ALTER INDEX` 문 실행 시 활성 상태인 모든 스냅샷 트랜잭션에 오류가 발생합니다. 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션은 영향을 받지 않습니다.  
  
    > [!NOTE]  
    > BULK INSERT 작업을 수행할 때 대상 테이블 메타데이터가 변경될 수 있습니다. 제약 조건 검사를 해제한 경우를 예로 들 수 있습니다. 이렇게 대상 테이블 메타데이터가 변경되면 동시 스냅샷 격리 트랜잭션이 대량 삽입된 테이블에 액세스할 수 없습니다.  
  
   
## <a name="customizing-locking-and-row-versioning"></a>잠금 및 행 버전 관리 사용자 지정  
  
### <a name="customizing-the-lock-time-out"></a>잠금 제한 시간 사용자 지정  
 다른 트랜잭션에서 이미 리소스에 대해 충돌되는 잠금을 소유하고 있어 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 인스턴스에서 트랜잭션에 잠금을 허가할 수 없는 경우 이 트랜잭션은 기존 잠금이 해제되기를 기다리면서 차단됩니다. 기본적으로 정해진 제한 시간은 없으며 리소스를 잠그기 전에 해당 리소스가 잠겨 있는지 여부를 확인할 수 없습니다. 단, 데이터에 대한 액세스를 시도할 수는 있으나 이로 인해 무기한으로 차단될 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 **sys.dm_os_waiting_tasks** 동적 관리 뷰를 사용하여 프로세스가 차단되었는지 여부와 프로세스를 차단하고 있는 주체를 확인할 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 **sp_who** 시스템 저장 프로시저를 사용합니다.  
  
 `LOCK_TIMEOUT` 설정을 사용하여 문이 차단된 리소스를 기다리는 최대 시간을 설정할 수 있습니다. 문이 LOCK_TIMEOUT 설정보다 오래 기다린 경우 차단된 문은 자동으로 취소되고 오류 메시지 1222(`Lock request time-out period exceeded`)가 애플리케이션으로 반환됩니다. 그러나 문을 포함하는 트랜잭션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 롤백되거나 취소되지 않습니다. 따라서 애플리케이션에는 오류 메시지 1222를 트래핑할 수 있는 오류 처리기가 있어야 합니다. 애플리케이션에서 오류를 트래핑하지 않으면 트랜잭션 내의 각 문이 취소된 것을 모르고 애플리케이션이 계속 진행하여 나중에 트랜잭션의 문이 실행되지 않은 문을 참조할 경우 오류가 발생할 수 있습니다.  
  
 오류 메시지 1222를 트래핑하는 오류 처리기를 구현하면 애플리케이션에서 시간 초과 상황을 처리하고 차단된 문을 자동으로 다시 전송하거나 전체 트랜잭션을 롤백하는 등의 해결 동작을 취할 수 있습니다.  
  
 현재 `LOCK_TIMEOUT` 설정을 확인하려면 `@@LOCK_TIMEOUT` 함수를 실행합니다.  
  
```sql  
SELECT @@lock_timeout;  
GO  
```  
  
### <a name="customizing-transaction-isolation-level"></a>트랜잭션 격리 수준 사용자 지정  
 READ COMMITTED는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 기본 격리 수준입니다. 애플리케이션을 다른 격리 수준에서 실행해야 하는 경우 다음과 같은 방법으로 격리 수준을 설정할 수 있습니다.  
  
-   [SET TRANSACTION ISOLATION LEVEL](../t-sql/statements/set-transaction-isolation-level-transact-sql.md) 문을 실행합니다.  
-   System.Data.SqlClient 관리 네임스페이스를 사용하는 ADO.NET 애플리케이션에서는 SqlConnection.BeginTransaction 메서드를 사용하여 *IsolationLevel* 옵션을 지정할 수 있습니다.  
-   ADO를 사용하는 애플리케이션에서는 `Autocommit Isolation Levels` 속성을 설정할 수 있습니다.  
-   OLE DB를 사용하는 애플리케이션에서는 트랜잭션을 시작할 때 *isoLevel* 을 원하는 트랜잭션 격리 수준으로 설정하고 ITransactionLocal::StartTransaction을 호출할 수 있습니다. 자동 커밋 모드에서 격리 수준을 지정할 때 OLE DB를 사용하는 애플리케이션에서는 DBPROPSET_SESSION 속성인 DBPROP_SESS_AUTOCOMMITISOLEVELS를 원하는 트랜잭션 격리 수준으로 설정할 수 있습니다.  
-   ODBC를 사용하는 애플리케이션에서는 SQLSetConnectAttr를 사용하여 SQL_COPT_SS_TXN_ISOLATION 특성을 설정할 수 있습니다.  
  
격리 수준을 지정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 세션에서 모든 쿼리와 DML(데이터 조작 언어) 문의 잠금 동작이 해당 격리 수준에서 작동합니다. 세션이 종료되거나 격리 수준을 다른 수준으로 설정할 때까지 해당 격리 수준이 적용됩니다.  
  
다음 예에서는 `SERIALIZABLE` 격리 수준을 설정합니다.  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
SELECT BusinessEntityID  
    FROM HumanResources.Employee;  
GO  
```  
  
필요에 따라 테이블 수준 힌트를 지정하여 개별 쿼리나 DML 문에 대해 격리 수준을 무시할 수 있습니다. 테이블 수준 힌트를 지정해도 세션의 다른 문에는 영향을 주지 않습니다. 꼭 필요한 경우에만 테이블 수준 힌트를 사용하여 기본 동작을 변경하는 것이 좋습니다.  
  
데이터를 읽을 때 공유 잠금을 요청하지 않는 수준으로 격리 수준이 설정된 경우에도 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 잠금을 획득해야 할 수 있습니다. 예를 들어 커밋되지 않은 읽기 격리 수준에서 실행되는 트랜잭션은 데이터를 읽을 때 공유 잠금을 획득하지 않지만 시스템 카탈로그 뷰를 읽을 때 잠금을 요청하는 경우도 있습니다. 즉 동시 트랜잭션이 해당 테이블의 메타데이터를 수정할 때 커밋되지 않은 읽기 트랜잭션이 테이블 쿼리를 차단할 수 있습니다.  
  
현재 설정된 트랜잭션 격리 수준을 확인하려면 다음 예와 같이 `DBCC USEROPTIONS` 문을 사용합니다. 이 결과 집합은 사용 중인 컴퓨터의 결과 집합과 다를 수 있습니다.  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
DBCC USEROPTIONS;  
GO  
```  
  
[!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```
Set Option                   Value  
---------------------------- -------------------------------------------  
textsize                     2147483647  
language                     us_english  
dateformat                   mdy  
datefirst                    7  
...                          ...  
Isolation level              repeatable read  
 
(14 row(s) affected)   
 
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```  
  
### <a name="locking-hints"></a>잠금 힌트  
 SELECT, INSERT, UPDATE 및 DELETE 문의 개별 테이블 참조에 대해 잠금 힌트를 지정할 수 있습니다. 힌트는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스가 테이블 데이터에 대해 사용하는 잠금 유형 또는 행 버전 관리를 지정합니다. 테이블 수준의 잠금 힌트는 개체에 대해 얻은 잠금 유형에 대해 더 세부적인 제어가 필요할 때 사용할 수 있습니다. 이러한 잠금 힌트는 세션에 대해 현재 트랜잭션 격리 수준을 무시합니다.  
  
 특정 잠금 힌트와 해당 동작에 대한 자세한 내용은 [Table Hints&#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-table.md)를 참조하십시오.  
  
> [!NOTE]  
> [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 거의 항상 올바른 잠금 수준을 선택합니다. 필요할 때만 테이블 수준의 잠금 힌트를 사용하여 기본 잠금 동작을 변경하는 것이 좋습니다. 잠금 수준의 허용을 취소하면 동시성에 영향을 줄 수 있습니다.  
  
 데이터를 읽을 때 공유 잠금 요청을 막는 잠금 힌트를 사용하여 SELECT를 처리하는 경우에도 메타데이터를 읽을 때 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 잠금을 획득해야 할 수 있습니다. 예를 들어 `NOLOCK` 힌트를 사용하는 `SELECT`는 데이터를 읽을 때 공유 잠금을 획득하지 않지만 시스템 카탈로그 뷰를 읽을 때는 경우에 따라 잠금을 요청할 수 있습니다. 즉, `NOLOCK`를 사용하는 `SELECT` 문을 차단할 수 있습니다.  
  
 다음 예와 같이 트랜잭션 격리 수준이 `SERIALIZABLE`로 설정되고 테이블 수준 잠금 힌트인 `NOLOCK`이 `SELECT` 문과 함께 사용되면 일반적으로 직렬화 가능 트랜잭션을 유지 관리하는 데 사용되는 키 범위 잠금이 적용되지 않습니다.  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT JobTitle  
    FROM HumanResources.Employee WITH (NOLOCK);  
GO  
  
-- Get information about the locks held by   
-- the transaction.  
SELECT    
        resource_type,   
        resource_subtype,   
        request_mode  
    FROM sys.dm_tran_locks  
    WHERE request_session_id = @@spid;  
  
-- End the transaction.  
ROLLBACK;  
GO  
```  
  
 `HumanResources.Employee`를 참조하는 유일한 잠금은 스키마 안정성(Sch-S) 잠금입니다. 이 경우 순차성은 더 이상 보장되지 않습니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 `ALTER TABLE`의 `LOCK_ESCALATION` 옵션에서 테이블 잠금을 선호하지 않을 수 있으며 분할된 테이블에 HoBT 잠금을 설정할 수 있습니다. 이 옵션은 잠금 힌트가 아니지만 잠금 에스컬레이션을 줄이는 데 사용할 수 있습니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
###  <a name="customizing-locking-for-an-index"></a><a name="Customize"></a> 인덱스 잠금 사용자 지정  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 대부분의 경우 쿼리에 가장 적합한 잠금 세분성을 자동으로 선택하는 동적 잠금 전략을 사용합니다. 페이지 잠금 및 행 잠금이 설정되어 있는 기본 잠금 수준은 잘 알려져 있으며 일관적인 테이블 또는 인덱스 액세스 패턴이 아닌 경우 및 리소스 충돌 문제를 해결해야 하는 경우 재정의하지 않는 것이 좋습니다. 잠금 수준을 재정의하면 테이블 또는 인덱스에 대한 동시 액세스에 심각한 방해가 될 수 있습니다. 예를 들어 사용자의 액세스가 빈번한 대규모 테이블에 테이블 수준 잠금만을 지정하는 경우, 사용자가 테이블에 액세스하려면 테이블 수준 잠금이 해제될 때까지 기다려야 하므로 병목 현상이 발생할 수 있습니다.  
  
 잘 알려져 있으며 일관된 액세스 패턴의 경우 페이지 잠금 또는 행 잠금을 허용하지 않는 것이 좋은 경우가 있습니다. 예를 들어 데이터베이스 애플리케이션에서 일괄 처리를 통해 매주 업데이트되는 조회 테이블을 사용하는 경우를 가정합니다. 동시 판독기는 공유(S) 잠금으로 테이블에 액세스하고, 주간 일괄 업데이트는 배타적(X) 잠금으로 테이블에 액세스합니다. 테이블에서 페이지 및 행 잠금을 해제하면 판독기가 공유 테이블 잠금을 통해 동시에 테이블에 액세스할 수 있어 주중 잠금 오버헤드가 줄어듭니다. 일괄 작업을 실행하면 배타적 테이블 잠금을 얻어 업데이트를 효율적으로 완료할 수 있습니다.  
  
 주간 일괄 업데이트는 업데이트 실행 동안 동시 판독기의 테이블 액세스를 차단하므로 페이지 및 행 잠금 해제가 허용될 수도, 그렇지 않을 수도 있습니다. 행 또는 페이지만 변경하는 일괄 작업의 경우, 행 또는 페이지 수준 잠금을 허용하도록 잠금 수준을 변경하여 다른 세션에서 차단 없이 테이블에서 읽기를 수행하도록 허용할 수 있습니다. 업데이트가 다수 포함된 일괄 작업의 경우, 테이블에 대한 배타적 잠금이 효율적인 일괄 작업 완수를 위한 최상의 방법일 수 있습니다.  
  
 2건의 동시 작업에서 모두 페이지 잠금이 필요하여 동일 테이블에서 행 잠금을 구한 다음 차단함에 따라 교착 상태가 발생하는 경우가 있습니다. 행 잠금을 허용하지 않으면 두 작업 중 하나를 대기시켜 교착 상태를 방지합니다.  
  
 인덱스에 사용되는 잠금의 세분성은 `CREATE INDEX` 및 `ALTER INDEX` 문을 사용하여 설정할 수 있습니다. 잠금 설정은 인덱스 페이지와 테이블 페이지에 모두 적용됩니다. 또한 `CREATE TABLE` 및 `ALTER TABLE` 문을 사용하여 `PRIMARY KEY` 및 `UNIQUE` 제약 조건에 대한 잠금 세분성을 설정할 수 있습니다. 이전 버전과의 호환성을 위해 `sp_indexoption` 시스템 저장 프로시저에서도 세분성을 설정할 수 있습니다. 특정 인덱스에 대한 현재 잠금 옵션을 표시하려면 `INDEXPROPERTY` 함수를 사용합니다. 페이지 수준 잠금, 행 수준 잠금 또는 페이지 수준 및 행 수준 잠금의 혼합 방법은 인덱스에 따라 허용되지 않을 수 있습니다.  
  
|허용되지 않는 잠금|허용되는 잠금|  
|----------------------|-----------------------|  
|페이지 수준|행 수준 및 테이블 수준 잠금|  
|행 수준|페이지 수준 및 테이블 수준 잠금|  
|페이지 수준 및 행 수준|테이블 수준 잠금|  
  
##  <a name="advanced-transaction-information"></a><a name="Advanced"></a> 고급 트랜잭션 정보  
  
### <a name="nesting-transactions"></a>중첩 트랜잭션  
 명시적 트랜잭션은 중첩할 수 있습니다. 중첩 트랜잭션은 주로 트랜잭션의 기존 프로세스나 활성 트랜잭션이 없는 프로세스에서 호출할 수 있는 저장 프로시저의 트랜잭션을 지원하기 위한 것입니다.  
  
 다음 예에서는 중첩된 트랜잭션의 용도를 보여 줍니다. *TransProc* 프로시저는 프로시저를 실행하는 프로세스의 트랜잭션 모드에 관계없이 트랜잭션을 강제 실행합니다. 트랜잭션이 활성 중일 때 *TransProc* 을 호출하면 *TransProc* 에서 중첩된 트랜잭션이 대부분 무시되고 바깥쪽 트랜잭션에서 수행된 최종 동작을 기준으로 `INSERT` 문이 커밋 또는 롤백됩니다. 처리 중인 트랜잭션이 없는 프로세스에서 `TransProc`를 실행하면 실제로 프로시저 마지막에서 `COMMIT TRANSACTION`가 `INSERT` 문이 커밋됩니다.  
  
```sql  
SET QUOTED_IDENTIFIER OFF;  
GO  
SET NOCOUNT OFF;  
GO  
CREATE TABLE TestTrans(Cola INT PRIMARY KEY,  
               Colb CHAR(3) NOT NULL);  
GO  
CREATE PROCEDURE TransProc @PriKey INT, @CharCol CHAR(3) AS  
BEGIN TRANSACTION InProc  
INSERT INTO TestTrans VALUES (@PriKey, @CharCol)  
INSERT INTO TestTrans VALUES (@PriKey + 1, @CharCol)  
COMMIT TRANSACTION InProc;  
GO  
/* Start a transaction and execute TransProc. */  
BEGIN TRANSACTION OutOfProc;  
GO  
EXEC TransProc 1, 'aaa';  
GO  
/* Roll back the outer transaction, this will  
   roll back TransProc's nested transaction. */  
ROLLBACK TRANSACTION OutOfProc;  
GO  
EXECUTE TransProc 3,'bbb';  
GO  
/* The following SELECT statement shows only rows 3 and 4 are   
   still in the table. This indicates that the commit  
   of the inner transaction from the first EXECUTE statement of  
   TransProc was overridden by the subsequent rollback. */  
SELECT * FROM TestTrans;  
GO  
```  
  
 안쪽 트랜잭션 커밋은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 무시합니다. 트랜잭션은 가장 바깥쪽 트랜잭션 마지막에 수행된 동작을 기준으로 커밋 또는 롤백됩니다. 바깥쪽 트랜잭션이 커밋되면 안쪽 중첩 트랜잭션도 커밋됩니다. 바깥쪽 트랜잭션이 롤백되면 안쪽 트랜잭션이 개별적으로 커밋되었는지에 관계없이 모든 안쪽 트랜잭션이 롤백됩니다.  
  
 `COMMIT TRANSACTION` 또는 `COMMIT WORK`에 대한 각 호출은 마지막으로 실행된 `BEGIN TRANSACTION`에 적용됩니다. `BEGIN TRANSACTION` 문을 중첩하면 `COMMIT` 문이 마지막으로 중첩된 트랜잭션, 즉 가장 안쪽의 트랜잭션에만 적용됩니다. 중첩된 트랜잭션 내의 `COMMIT TRANSACTION` *transaction_name* 문이 바깥쪽 트랜잭션의 트랜잭션 이름을 참조해도 커밋은 가장 안쪽의 트랜잭션에만 적용됩니다.  
  
 `ROLLBACK TRANSACTION` 문의 *transaction_name* 매개 변수는 명명된 중첩 트랜잭션 집합의 안쪽 트랜잭션을 참조할 수 없습니다. *transaction_name* 은 가장 바깥쪽 트랜잭션의 트랜잭션 이름만 참조할 수 있습니다. 바깥쪽 트랜잭션의 이름을 사용하는 ROLLBACK TRANSACTION *transaction_name* 문이 중첩 트랜잭션 집합의 특정 수준에서 실행되면 중첩된 트랜잭션이 모두 롤백됩니다. `ROLLBACK WORK` 또는 `ROLLBACK TRANSACTION` 문이 *transaction_name* 매개 변수 없이 중첩 트랜잭션 집합의 특정 수준에서 실행되면 가장 바깥쪽 트랜잭션을 포함하여 모든 중첩 트랜잭션이 롤백됩니다.  
  
 `@@TRANCOUNT` 함수는 현재 트랜잭션 중첩 수준을 기록합니다. 각 `BEGIN TRANSACTION` 문은 `@@TRANCOUNT`를 1씩 증가시킵니다. `COMMIT TRANSACTION` 또는 `COMMIT WORK` 문은 각기 `@@TRANCOUNT`을 1씩 감소시킵니다. 트랜잭션 이름이 없는 `ROLLBACK WORK` 또는 `ROLLBACK TRANSACTION` 문은 모든 중첩 트랜잭션을 롤백하고 `@@TRANCOUNT`을 0으로 되돌립니다. 중첩 트랜잭션 집합에서 가장 바깥쪽 트랜잭션의 트랜잭션 이름을 사용하는 `ROLLBACK TRANSACTION`은 모든 중첩 트랜잭션을 롤백하고 `@@TRANCOUNT`를 0으로 되돌립니다. 트랜잭션 안에 있는지 확실하지 않을 때는 `SELECT @@TRANCOUNT`을 조회하여 1 이상인지 확인합니다. `@@TRANCOUNT`이 0이면 트랜잭션 밖에 있는 것입니다.  
  
### <a name="using-bound-sessions"></a>바운드 세션 사용  
 바운드 세션을 통해 같은 서버의 여러 세션 간에 동작을 편리하게 조정할 수 있습니다. 바운드 세션을 사용하면 두 개 이상의 세션에서 같은 트랜잭션과 잠금을 공유할 수 있으며 여러 바운드 세션이 잠금 충돌 없이 같은 데이터 작업을 수행할 수 있습니다. 바운드 세션은 같은 애플리케이션 내의 여러 세션에서 생성되거나 개별 세션의 여러 애플리케이션에서 생성될 수 있습니다.  
  
 바운드 세션에 참여하려면 세션에서 개방형 Data Services를 통한 `sp_getbindtoken` 또는 `srv_getbindtoken`를 호출하여 바인드 토큰을 가져와야 합니다. 바인드 토큰은 각 바운드 트랜잭션을 고유하게 식별하는 문자열입니다. 가져온 바인드 토큰은 현재 세션과 바인딩할 다른 세션으로 전송됩니다. 다른 세션은 첫 번째 세션으로부터 받은 바인드 토큰으로 **sp_bindsession** 을 호출하여 트랜잭션에 바인딩합니다.  
  
> [!NOTE]  
> `sp_getbindtoken` 또는 `srv_getbindtoken`가 성공하려면 세션에 활성 사용자 트랜잭션이 있어야 합니다.  
  
 애플리케이션 코드에 대한 첫 번째 세션을 만들고 애플리케이션 코드의 세션을 첫 번째 세션에 바인딩하는 애플리케이션 코드에서 바인드 토큰을 전송해야 합니다. 애플리케이션이 다른 프로세스에서 시작한 트랜잭션에 대한 바인드 토큰을 얻을 수 있는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이나 API 함수는 없습니다. 다음과 같은 방법으로 바인드 토큰을 전송할 수 있습니다.  
  
-   세션이 모두 같은 애플리케이션 프로세스에서 시작되는 경우에는 바인드 토큰을 글로벌 메모리에 저장하거나 매개 변수로 함수에 전달할 수 있습니다.  
  
-   세션이 개별 애플리케이션 프로세스에서 생성되는 경우에는 RPC(원격 프로시저 호출)나 DDE(동적 데이터 교환) 등의 IPC(프로세스 간 통신)를 사용하여 바인드 토큰을 전송할 수 있습니다.  
  
-   첫 번째 세션에 바인딩하려는 세션에서 읽을 수 있는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스의 테이블에 바인드 토큰을 저장할 수 있습니다.  
  
 항상 바운드 세션 집합의 한 세션만 활성화될 수 있습니다. 세션이 인스턴스에서 문을 실행하고 있거나 인스턴스로부터 보류 중인 결과를 받으면 이 세션에 연결된 다른 세션은 현재 세션이 처리를 마치거나 현재 문을 취소할 때까지 해당 인스턴스에 액세스할 수 없습니다. 인스턴스가 다른 바운드 세션의 문을 처리하고 있으면 트랜잭션 공간이 사용 중이므로 나중에 세션을 다시 시도해야 함을 나타내는 오류가 발생합니다.  
  
 세션을 바인딩할 때 각 세션의 해당 격리 수준 설정이 유지됩니다. SET TRANSACTION ISOLATION LEVEL을 사용하여 한 세션의 격리 수준 설정을 변경해도 이 세션에 바인딩된 다른 세션의 설정에는 영향을 주지 않습니다.  
  
#### <a name="types-of-bound-sessions"></a>바운드 세션 유형  
 바운드 세션에는 로컬과 분산의 두 가지 유형이 있습니다.  
  
-   **로컬 바운드 세션**  
    여러 바운드 세션이 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 단일 인스턴스에서 단일 트랜잭션의 트랜잭션 공간을 공유할 수 있습니다.  
  
-   **분산 바운드 세션**  
    MS DTC([!INCLUDE[msCoName](../includes/msconame-md.md)] Distributed Transaction Coordinator)를 사용하여 전체 트랜잭션을 커밋하거나 롤백할 때까지 여러 바운드 세션이 둘 이상의 인스턴스에서 같은 트랜잭션을 공유할 수 있습니다.  
  
 분산 바운드 세션은 문자열 바인드 토큰으로 식별되지 않고 분산 트랜잭션 식별 번호로 식별됩니다. 바운드 세션이 로컬 트랜잭션과 관련되어 있고 원격 서버에서 `SET REMOTE_PROC_TRANSACTIONS ON`을 ON으로 설정하여 RPC를 실행하는 경우에는 MS DTC에 의해 로컬 바운드 트랜잭션이 분산 바운드 트랜잭션으로 자동 승격되고 MS DTC 세션이 시작됩니다.  
  
#### <a name="when-to-use-bound-sessions"></a>바운드 세션 사용 시기  
 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 바운드 세션은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 호출하는 프로세스를 대신하여 이 문을 실행해야 하는 확장 저장 프로시저를 개발하는 데 주로 사용되었습니다. 호출 프로세스에서 바인드 토큰을 확장 저장 프로시저의 한 매개 변수로 전달하도록 설정하면 프로시저가 호출 프로세스의 트랜잭션 공간에 참여하여 호출 프로시저와 확장 저장 프로시저가 통합됩니다.  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 저장 프로시저를 CLR로 작성하여 확장 저장 프로시저보다 뛰어난 안전성, 확장성 및 안정성을 제공합니다. CLR 저장 프로시저는 **SqlContext** 개체를 사용하여 `sp_bindsession`이 아닌 호출 세션의 컨텍스트에 참여합니다.  
  
 바운드 세션을 사용하여 단일 업무 트랜잭션에서 함께 작업하는 여러 개별 프로그램에 비즈니스 논리가 통합되는 3계층 애플리케이션을 개발할 수 있습니다. 이러한 프로그램의 경우 데이터베이스 액세스를 잘 조정하도록 코드를 작성해야 합니다. 두 세션이 같은 잠금을 공유하기 때문에 두 프로그램이 동시에 같은 데이터를 수정할 수 없습니다. 항상 한 세션만 트랜잭션의 일부로 작업을 수행할 수 있으므로 병렬 실행은 불가능합니다. 모든 DML 문이 완료되어 결과가 검색된 경우와 같이 잘 정의된 양보점(yield point)에서만 세션 간에 트랜잭션이 전환될 수 있습니다.  
  
### <a name="coding-efficient-transactions"></a>효율적인 트랜잭션 코딩  
 트랜잭션을 되도록 짧게 유지하는 것이 중요합니다. 트랜잭션이 시작되면 DBMS(데이터베이스 관리 시스템)가 트랜잭션이 끝날 때까지 많은 리소스를 보유하여 트랜잭션의 ACID(원자성, 일관성, 격리성, 영속성) 속성을 보호합니다. 데이터가 수정되면 다른 트랜잭션이 읽을 수 없도록 수정된 행이 배타적 잠금으로 보호되어야 하며 트랜잭션이 커밋되거나 롤백될 때까지 배타적 잠금이 유지되어야 합니다. 트랜잭션 격리 수준 설정에 따라 `SELECT` 문에서 트랜잭션이 커밋 또는 롤백될 때까지 보유해야 하는 잠금을 획득할 수 있습니다. 특히 많은 사용자가 사용하는 시스템에서는 트랜잭션을 되도록 짧게 유지하여 동시 연결 간에 리소스에 대한 잠금 경합을 줄여야 합니다. 실행 시간이 긴 비효율적인 트랜잭션은 사용자 수가 적을 때는 별로 문제가 되지 않지만 사용자가 많을 때는 심각한 문제가 됩니다. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]부터 지연된 영구 트랜잭션이 지원됩니다. 지연된 내구성 있는 트랜잭션은 내구성을 보장하지 않습니다. 자세한 내용은 [트랜잭션 내구성](../relational-databases/logs/control-transaction-durability.md) 항목을 참조하세요.  
  
#### <a name="coding-guidelines"></a><a name="guidelines"></a> 코딩 지침  
 효율적인 트랜잭션을 코딩하려면 다음 지침을 참조하십시오.  
  
-   트랜잭션 중 사용자로부터 입력을 요청하지 마십시오.  
    트랜잭션이 시작되기 전에 사용자로부터 필요한 입력 내용을 모두 입력받아야 합니다. 트랜잭션 중 추가 사용자 입력이 필요하면 현재 트랜잭션을 롤백하고 사용자 입력이 제공된 후 트랜잭션을 다시 시작해야 합니다. 사용자가 즉시 응답하더라도 사람의 반응 속도는 컴퓨터 속도보다 매우 느립니다. 트랜잭션에 의해 보유된 모든 리소스는 꽤 긴 시간 동안 보유되므로 차단 문제가 발생할 수 있습니다. 사용자가 응답하지 않으면 응답할 때까지 몇 분 또는 몇 시간 동안 트랜잭션이 계속 활성 상태로 남아 있고 중요한 리소스가 잠겨 있게 됩니다.  
  
-   가능하면 데이터를 찾아보는 동안에는 트랜잭션을 열지 마십시오.  
    모든 예비 데이터 분석이 완료될 때까지 트랜잭션을 시작하지 말아야 합니다.  
  
-   트랜잭션을 되도록 짧게 유지합니다.  
    수정해야 한다고 판단되면 트랜잭션을 시작하고 수정 문을 실행한 다음 즉시 커밋 또는 롤백합니다. 필요할 때까지는 트랜잭션을 열지 마십시오.  
  
-   차단을 줄이려면 읽기 전용 쿼리에 행 버전 관리 기반의 격리 수준을 사용합니다.  
  
-   낮은 트랜잭션 격리 수준을 효율적으로 사용하십시오.  
    대부분의 애플리케이션은 커밋된 읽기 트랜잭션 격리 수준을 사용하도록 코딩할 수 있습니다. 모든 트랜잭션에서 직렬화 가능 트랜잭션 격리 수준이 필요한 것은 아닙니다.  
  
-   낙관적 동시성 옵션과 같이 낮은 커서 동시성 옵션을 효율적으로 사용합니다.  
    동시 업데이트 가능성이 적은 시스템에서는 한 사용자가 데이터를 읽은 후 다른 사용자가 해당 데이터를 변경하여 발생하는 오류를 처리하는 오버헤드가 데이터를 읽을 때마다 행을 잠그는 오버헤드보다 훨씬 적을 수 있습니다.  
  
-   트랜잭션에서는 가능한 적은 양의 데이터에 액세스합니다.  
    이렇게 하면 잠긴 행 수가 줄어들어 트랜잭션 간의 경합이 감소됩니다.  
    
-   가능하면 보류 잠금과 같은 비관적 잠금 힌트를 사용하지 않습니다. 
    HOLDLOCK 또는 SERIALIZABLE 격리 수준과 같은 힌트를 사용하면 프로세스가 공유 잠금에서도 대기하여 동시성이 감소할 수 있습니다.

-   가능하면 암시적 트랜잭션을 사용하지 않습니다. 암시적 트랜잭션의 특성 때문에 예기치 않은 동작이 발생할 수 있습니다. [암시적 트랜잭션 및 동시성 문제](#implicit-transactions-and-avoiding-concurrency-and-resource-problems)를 참조하세요.

-   [채우기 비율](indexes/specify-fill-factor-for-an-index.md)을 줄여 인덱스를 설계합니다. 채우기 비율을 줄이면 인덱스 페이지의 조각화를 방지하거나 줄여 특히 디스크에서 검색할 때 인덱스 검색 시간을 줄일 수 있습니다. 테이블 또는 뷰의 데이터와 인덱스에 대한 조각화 정보를 보려면 sys.dm_db_index_physical_stats를 사용합니다. 
  
#### <a name="implicit-transactions-and-avoiding-concurrency-and-resource-problems"></a>암시적 트랜잭션과 동시성 및 리소스 문제 방지  
 동시성 문제와 리소스 문제를 방지하려면 암시적 트랜잭션을 신중하게 관리합니다. 암시적 트랜잭션을 사용할 때는 `COMMIT` 또는 `ROLLBACK` 다음의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 자동으로 새 트랜잭션을 시작합니다. 이로 인해 애플리케이션에서 데이터를 찾아보는 동안이나 사용자 입력이 필요할 때 새 트랜잭션이 열릴 수 있습니다. 데이터 수정을 보호하는 데 필요한 마지막 트랜잭션을 완료한 다음 데이터 수정을 보호하기 위해 트랜잭션이 다시 한 번 필요할 때까지 암시적 트랜잭션을 해제합니다. 이렇게 하면 애플리케이션에서 데이터를 찾아보고 사용자로부터 입력을 받는 동안 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]이 자동 커밋 모드를 사용할 수 있습니다.  
  
 또한 스냅샷 격리 수준을 사용하면 새 트랜잭션이 잠금을 확보하지 않더라도 장기 실행 트랜잭션이 `tempdb`에서 이전 버전이 제거되지 않도록 방지합니다.  
  
### <a name="managing-long-running-transactions"></a>장기 실행 트랜잭션 관리  
 *장기 실행 트랜잭션* 은 제때에 커밋되거나 롤백되지 않은 활성 트랜잭션입니다. 예를 들어 트랜잭션의 시작과 끝을 사용자가 제어하는 경우에는 대개 사용자가 트랜잭션을 시작한 후 트랜잭션에서 사용자의 응답을 기다리는 동안 자리를 비울 때 장기 실행 트랜잭션이 발생합니다.  
  
 장기 실행 트랜잭션으로 인해 데이터베이스에 대해 다음과 같은 심각한 문제가 발생할 수 있습니다.  
  
-   활성 트랜잭션이 커밋되지 않은 많은 수정 작업을 수행한 후에 서버 인스턴스가 종료되면 서버 인스턴스가 다시 시작된 후의 복구 단계 수행 시 **recovery interval** 서버 구성 옵션 또는 `ALTER DATABASE ... SET TARGET_RECOVERY_TIME`. 이러한 옵션은 활성 검사점 및 간접 검사점의 빈도를 각각 지정합니다. 검사점 형식에 대한 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.  
  
-   무엇보다도 대기 중인 트랜잭션은 로그를 거의 생성하지 않을 수 있지만 로그 잘림을 무한정 방해하여 트랜잭션 로그가 커져 가득 찰 수 있습니다. 트랜잭션 로그가 꽉 차면 데이터베이스에서 업데이트를 더 이상 수행할 수 없습니다. 자세한 내용은 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md), [전체 트랜잭션 로그 문제 해결&#40;SQL Server Error 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md) 및 [트랜잭션 로그&#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
#### <a name="discovering-long-running-transactions"></a>장기 실행 트랜잭션 검색  
 장기 실행 트랜잭션을 찾으려면 다음 중 하나를 사용합니다.  
  
-   **sys.dm_tran_database_transactions**  
  
    이 동적 관리 뷰는 데이터베이스 수준에서 트랜잭션 정보를 반환합니다. 장기 실행 트랜잭션과 특히 관련된 열에는 첫 번째 로그 레코드 시간(**database_transaction_begin_time**), 현재 트랜잭션 상태(**database_transaction_state**), 트랜잭션 로그(**database_transaction_begin_lsn**)에서 시작 레코드의 LSN(로그 시퀀스 번호) 등이 있습니다.  
  
    자세한 내용은 [sys.dm_tran_database_transactions&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)를 참조하세요.  
  
-   `DBCC OPENTRAN`  
  
    이 문을 사용하면 트랜잭션 소유자의 사용자 ID를 식별할 수 있으므로 트랜잭션의 출처를 추적하여 롤백 대신 커밋을 더 많이 수행하는 순차적 종료 작업을 확인할 수 있습니다. 자세한 내용은 [DBCC OPENTRAN&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)을 참조하세요.  
  
#### <a name="stopping-a-transaction"></a>트랜잭션 중지  
 KILL 문을 사용해야 하는 경우도 있습니다. 그러나 특히 중요한 프로세스가 실행 중일 때는 이 문을 신중하게 사용하십시오. 자세한 내용은 [KILL&#40;Transact-SQL&#41;](../t-sql/language-elements/kill-transact-sql.md)을 참조하세요.  
  
##  <a name="additional-reading"></a><a name="Additional_Reading"></a> 더 보기   
[행 버전 관리 오버헤드](/archive/blogs/sqlserverstorageengine/overhead-of-row-versioning)   
[확장 이벤트](../relational-databases/extended-events/extended-events.md)   
[sys.dm_tran_locks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)     
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)      
[트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)