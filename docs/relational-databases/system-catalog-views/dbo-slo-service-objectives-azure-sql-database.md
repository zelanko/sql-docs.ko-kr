---
title: "dbo.slo_service_objectives (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f91dccf478821047e4c3a25ea19d35d1a2774fd
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  이 기능은 미리 보기 상태에서 이며 사용 되지 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 합니다. 이 기능은 향후 릴리스에서 변경되거나 제거될 수 있으므로 이 기능의 특정 구현에 의존하지 마세요.  
  
 현재 서버에 대한 SLO(서비스 수준 목표) 정보를 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 합니다.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|서비스 수준 목표의 ID입니다.|  
|NAME|**sysname**|서비스 수준 목표의 이름입니다.|  
|description|**nvarchar**|서비스 수준 목표에 대한 설명입니다.|  
|create_date|**datetimeoffset(7)**|서버에 대한 서비스 수준 목표를 만든 날짜입니다.|  
|is_system|**bit**|1 = 시스템 서비스 수준 목표|  
|is_default|**bit**|1 = 서비스 수준 목표가 기본 SLO입니다.|  
|state|**tinyint**|1 = 서비스 수준 목표가 설정되었습니다.<br /><br /> 2 = 서비스 수준 목표가 해제되었습니다.|  
|state_desc|**nvarchar**|서비스 수준 목표에 대한 설명입니다.|  
|metadata_version|**decimal**|서비스 수준 목표의 버전입니다.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰는 가상에 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있는 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Premium 데이터베이스 관리](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
