---
title: sys.spatial_reference_systems (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4490cc6d28ee06193436de8b57cde8e7ac04402
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysspatialreferencesystems-transact-sql"></a>sys.spatial_reference_systems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 공간 참조 시스템(SRID)을 나열합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 SRID입니다.|  
|authority_name|**nvarchar (128)**|SRID의 인증 기관입니다.|  
|authorized_spatial_reference_id|**int**|SRID의 인증 기관에서 제공한 **authority_name**합니다.|  
|well_known_text|**nvarchar(4000)**|SRID의 WKT 표현입니다.|  
|unit_of_measure|**nvarchar (128)**|측정 단위 이름입니다.|  
|unit_conversion_factor|**float**|미터 단위의 측정 단위 길이입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
