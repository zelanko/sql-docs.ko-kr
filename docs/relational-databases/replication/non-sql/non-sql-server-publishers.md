---
description: SQL Server 이외 게시자
title: SQL Server 이외 게시자 | Microsoft 문서
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9560875e4db3a644644238b0140fadb33cf1877d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420447"
---
# <a name="non-sql-server-publishers"></a>SQL Server 이외 게시자  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 원본에서 데이터를 게시하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 데이터를 통합할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 Oracle 데이터베이스에서 게시된 스냅샷 또는 트랜잭션 데이터를 구독할 수 있습니다. Oracle에서 게시에 대한 자세한 내용은 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 트랜잭션 및 스냅샷 복제에 대해 다음과 같이 다른 유형의 시나리오를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자로 데이터 게시  

-   Oracle에서 데이터를 게시할 때 다음과 같은 제한 사항이 있습니다.  

  |복제 |2016 또는 이전 버전 |2017 이상 |
  |:-----------|:---------------|:-------------|
  |Oracle에서 복제 |Oracle 10g 또는 이전 버전만 지원 |Oracle 10g 또는 이전 버전만 지원 |
  |Oracle로 복제 |Oracle 12c까지 |지원되지 않음 |
  | &nbsp; | &nbsp; | &nbsp; |


 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스에서 게시 작업은 다음과 같은 시나리오에서 유용합니다.  
  
|시나리오|설명|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 애플리케이션 배포|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 이외 데이터베이스에서 복제한 데이터 작업 시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Visual Studio 및[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하여 개발합니다.|  
|데이터 웨어하우징 준비 서버(staging server)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 준비 데이터베이스와[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스의 동기화를 유지합니다.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|원본 시스템의 변경 내용을 복제하면서 실시간으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 애플리케이션을 테스트합니다. 마이그레이션에 만족하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 전환합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
