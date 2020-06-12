---
title: 복제 뷰 (Transact-sql) | Microsoft Docs
description: 복제 뷰에는 SQL Server에서 복제에 사용 되는 정보가 포함 되어 있습니다. 이 뷰를 사용하면 복제 시스템 테이블의 데이터에 보다 쉽게 액세스할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: ae0c1245bdf9ff7fe1d1eb712745cbc15d2479af
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807932"
---
# <a name="replication-views-transact-sql"></a>복제 뷰(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이러한 뷰에는의 복제에 사용 되는 정보가 포함 되어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다. 뷰를 사용 하면 [복제 시스템 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)의 데이터에 쉽게 액세스할 수 있습니다. 사용자 데이터베이스가 게시 또는 구독 데이터베이스로 사용될 때 이 데이터베이스에 뷰가 생성됩니다. 복제 토폴로지에서 데이터베이스가 제거되면 사용자 데이터베이스에서 모든 복제 개체가 제거됩니다. 복제 메타 데이터에 액세스 하는 기본 방법은 [복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 사용 하는 것입니다.  
  
> [!IMPORTANT]  
>  어떤 사용자도 시스템 뷰를 직접 변경해서는 안 됩니다.  
  
## <a name="replication-views"></a>복제 뷰  
 다음은 복제에서 사용되고 데이터베이스에 의해 그룹화되는 시스템 뷰의 목록입니다.  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb 데이터베이스의 복제 뷰  
  
|||  
|-|-|  
|[Transact-sql&#41;MSdatatype_mappings &#40;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[msdb.dbo.sysdatatypemappings &#40;Transact-sql&#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>배포 데이터베이스의 복제 뷰  
  
|||  
|-|-|  
|[IHextendedArticleView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40;시스템 뷰&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[IHextendedSubscriptionView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40;Transact-sql&#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications&#40;시스템 뷰&#41;&#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[Transact-sql&#41;MSdistribution_status &#40;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions&#40;시스템 뷰&#41;&#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40;시스템 뷰&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>게시 데이터베이스의 복제 뷰  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>구독 데이터베이스의 복제 뷰  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
