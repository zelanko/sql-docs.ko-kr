---
title: sys.spatial_reference_systems (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f1cb77a5da692f17a790d2eb5ffca6f82a939449
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39538293"
---
# <a name="sysspatialreferencesystems-transact-sql"></a>sys.spatial_reference_systems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 공간 참조 시스템(SRID)을 나열합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 SRID입니다.|  
|authority_name|**nvarchar(128)**|SRID의 인증 기관입니다.|  
|authorized_spatial_reference_id|**int**|에 명명 된 기관에 의해 지정 된 SRID **authority_name**합니다.|  
|well_known_text|**nvarchar(4000)**|SRID의 WKT 표현입니다.|  
|unit_of_measure|**nvarchar(128)**|측정 단위 이름입니다.|  
|unit_conversion_factor|**float**|미터 단위의 측정 단위 길이입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
