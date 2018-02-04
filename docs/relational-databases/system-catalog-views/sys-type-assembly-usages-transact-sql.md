---
title: sys.type_assembly_usages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.type_assembly_usages
- sys.type_assembly_usages_TSQL
- type_assembly_usages_TSQL
- type_assembly_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.type_assembly_usages catalog view
ms.assetid: 79b8bf25-6e4e-4a07-ae93-7a4e44f65171
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3ce4d7e61fb608e44d5ef9f218449981d7d49c1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="systypeassemblyusages-transact-sql"></a>sys.type_assembly_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  어셈블리 참조에 대한 각 유형당 한 개의 행을 포함합니다.  
  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**user_type_id**|**int**|유형의 ID입니다.<br /><br /> 형식의 이름을 반환 하려면에 가입는 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에서이 열에 있습니다.|  
|**assembly_id**|**int**|어셈블리의 ID입니다.|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [스칼라 유형 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
