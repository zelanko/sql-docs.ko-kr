---
title: 다른 유형의 데이터베이스 복제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 40
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3c012c14c3d388617dc8dca3b2137f69a007a268
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185168"
---
# <a name="heterogeneous-database-replication"></a>다른 유형의 데이터베이스 복제
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 트랜잭션 및 스냅숏 복제에 대해 다음과 같이 다른 유형의 시나리오를 지원합니다.  
  
-   Oracle에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 데이터 게시  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자로 데이터 게시  
  
 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Oracle에서 데이터 게시  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하여 Oracle에서 데이터를 게시할 수 있습니다. 이때 대부분의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스냅숏 및 트랜잭션 복제 기능을 동일한 방식으로 간단하게 사용할 수 있습니다. 다음 시나리오에 대해서는 Oracle에서 데이터를 게시하는 것이 가장 적합합니다.  
  
|시나리오|Description|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 응용 프로그램 배포|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 이외 데이터베이스에서 복제한 데이터 작업 시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Visual Studio 및[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하여 개발합니다.|  
|데이터 웨어하우징 준비 서버(staging server)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 준비 데이터베이스와[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스의 동기화를 유지합니다.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|원본 시스템의 변경 내용을 복제하면서 실시간으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 응용 프로그램을 테스트합니다. 마이그레이션에 만족하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 전환합니다.|  
  
 자세한 내용은 [Oracle 게시 개요](oracle-publishing-overview.md)를 참조하세요.  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>SQL Server 이외 구독자에 데이터 게시  
 다음[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스는 스냅숏 및 트랜잭션 게시의 구독자로 지원됩니다.  
  
-   Oracle에서 지원하는 모든 플랫폼용 Oracle 제품  
  
-   AS400, MVS, Unix, Linux 및 Windows용 IBM DB2  
  
 자세한 내용은 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)을(를) 참조하세요.  
  
  