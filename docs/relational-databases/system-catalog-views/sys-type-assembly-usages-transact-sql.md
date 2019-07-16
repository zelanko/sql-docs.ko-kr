---
title: sys.type_assembly_usages (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 48dbb35fcecde99dad30e71fdcd2c85a2ab92e3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061280"
---
# <a name="systypeassemblyusages-transact-sql"></a>sys.type_assembly_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  어셈블리 참조에 대한 각 유형당 한 개의 행을 포함합니다.  
  

  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**user_type_id**|**int**|유형의 ID입니다.<br /><br /> 연결할 형식의 이름을 반환할 합니다 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에이 열입니다.|  
|**assembly_id**|**int**|어셈블리의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [스칼라 유형 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
