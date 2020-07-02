---
title: sys. module_assembly_usages (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- module_assembly_usages_TSQL
- module_assembly_usages
- sys.module_assembly_usages_TSQL
- sys.module_assembly_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.module_assembly_usages catalog view
ms.assetid: b0f9ffab-6ac7-49d5-8369-477fa6b1c02b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 43b62d07d41a40619f85fd615e9c901d7172dfe8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760351"
---
# <a name="sysmodule_assembly_usages-transact-sql"></a>sys.module_assembly_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  모듈에서 어셈블리로의 각 참조에 대해 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL 개체의 식별 번호입니다. 데이터베이스 내에서 고유합니다.|  
|**assembly_id**|**int**|이 모듈이 생성된 어셈블리의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
