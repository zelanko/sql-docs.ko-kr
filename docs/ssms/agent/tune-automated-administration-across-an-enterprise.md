---
description: 기업 내의 자동화된 관리 튜닝
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
ms.openlocfilehash: 6fbb2e883e77ed797fb367c3624429c2b1a4d720
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038734"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>기업 내의 자동화된 관리 튜닝

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 통해 다중 서버를 관리할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 자체 튜닝 기능을 사용할 수 있습니다. 따라서 정상 조건에서 추가 작업 튜닝은 필요하지 않습니다. 그러나 작업을 실행하고 경고를 생성하고 운영자에게 알릴 때 네트워크 로드가 증가됩니다. 기업 내에서 자동화된 관리를 튜닝하여 이러한 작업으로 인한 네트워크 트래픽을 최소화할 수 있습니다.  

## <a name="see-also"></a>참고 항목

[데이터 흐름 엔진의 성능 모니터링](../../integration-services/performance/performance-counters.md)