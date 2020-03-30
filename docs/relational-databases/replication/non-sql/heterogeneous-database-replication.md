---
title: 다른 유형의 데이터베이스 복제 | Microsoft 문서
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6c7393b7cad97c613bf288d2f9e49e5922842e0b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67900976"
---
# <a name="heterogeneous-database-replication"></a>다른 유형의 데이터베이스 복제  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 트랜잭션 및 스냅샷 복제에 대해 다음과 같이 다른 유형의 시나리오를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자로 데이터 게시  

-   Oracle에서 데이터를 게시할 때 다음과 같은 제한 사항이 있습니다.  

  | |2016 또는 이전 버전 |2017 이상 |
  |-------|-------|--------|
  |Oracle에서 복제 |Oracle 10g 또는 이전 버전만 지원 |Oracle 10g 또는 이전 버전만 지원 |
  |Oracle로 복제 |Oracle 12c까지 |지원되지 않음 |


 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Oracle에서 데이터 게시  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하여 Oracle에서 데이터를 게시할 수 있습니다. 이때 대부분의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스냅샷 및 트랜잭션 복제 기능을 동일한 방식으로 간단하게 사용할 수 있습니다. 이 기능을 사용하려면 Oracle 버전 10G 또는 이전 버전이 필요합니다. 다음 시나리오에 대해서는 Oracle에서 데이터를 게시하는 것이 가장 적합합니다.  
  
|시나리오|Description|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 애플리케이션 배포|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 이외 데이터베이스에서 복제한 데이터 작업 시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Visual Studio 및[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하여 개발합니다.|  
|데이터 웨어하우징 준비 서버(staging server)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 준비 데이터베이스와[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스의 동기화를 유지합니다.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|원본 시스템의 변경 내용을 복제하면서 실시간으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 애플리케이션을 테스트합니다. 마이그레이션에 만족하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 전환합니다.|  
  
 자세한 내용은 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)를 참조하세요.  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>SQL Server 이외 구독자에 데이터 게시  
 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스는 스냅샷 및 트랜잭션 게시의 구독자로 지원됩니다.  
  
-   Oracle에서 지원하는 모든 플랫폼용 Oracle 제품  
  
-   AS400, MVS, Unix, Linux 및 Windows용 IBM DB2  
  
 자세한 내용은 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.  
  
  
