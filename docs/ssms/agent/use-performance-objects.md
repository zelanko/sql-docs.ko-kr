---
title: 성능 개체 사용 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 01d245a9ac6eb32bd38978bd2ed4189f774332ca
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982415"
---
# <a name="use-performance-objects"></a>성능 개체 사용
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에는 서비스 수행 방법을 모니터링하는 성능 개체와 카운터가 포함됩니다. 이러한 성능 개체를 사용하면 Windows 도구인 성능 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 백그라운드에서 수행하는 작업을 식별할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 현재 실행 중인 활성 작업 수를 확인하여 차단된 작업을 식별할 수 있습니다.  
  
컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 성능 개체와 카운터가 있습니다. 성능 개체는 각 개체가 나타내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 따라 이름이 지정됩니다.  
  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 성능 개체의 이름 지정 방법을 보여 줍니다.  
  
|인스턴스 유형|개체 이름|  
|-----------------|---------------|  
|Default|**SQLAgent:***object*:*counter*|  
|명명된 형식|**SQLAgent$**<br /> **&#42;instance_name&#42; :***object*:*counter*|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 성능 개체가 포함됩니다.  
  
|개체 이름|설명|  
|---------------|---------------|  
|[SQLAgent:Jobs](http://msdn.microsoft.com/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|시작된 작업, 성공률 및 현재 상태에 대한 성능 정보|  
|[SQLAgent:JobSteps](http://msdn.microsoft.com/44f9983c-1753-4fe0-8475-973aa2460b3a)|작업 단계에 대한 상태 정보|  
|[SQLAgent:Alerts](http://msdn.microsoft.com/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|경고 및 알림 수에 대한 정보|  
|[SQLAgent:Statistics](http://msdn.microsoft.com/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|일반 성능 정보|  
  
## <a name="see-also"></a>참고 항목  
[성능 모니터링 및 튜닝](http://msdn.microsoft.com/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[방법: 시스템 모니터 시작(Windows)](http://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
