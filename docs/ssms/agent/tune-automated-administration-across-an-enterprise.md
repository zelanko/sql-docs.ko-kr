---
title: 기업 내의 자동화된 관리 튜닝
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b43a1298c16ba1e51459852f8c775dd67b5b4a7b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755030"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>기업 내의 자동화된 관리 튜닝

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 통해 다중 서버를 관리할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 자체 튜닝 기능을 사용할 수 있습니다. 따라서 정상 조건에서 추가 작업 튜닝은 필요하지 않습니다. 그러나 작업을 실행하고 경고를 생성하고 운영자에게 알릴 때 네트워크 로드가 증가됩니다. 기업 내에서 자동화된 관리를 튜닝하여 이러한 작업으로 인한 네트워크 트래픽을 최소화할 수 있습니다.  

## <a name="see-also"></a>참고 항목

[데이터 흐름 엔진의 성능 모니터링](../../integration-services/performance/performance-counters.md)