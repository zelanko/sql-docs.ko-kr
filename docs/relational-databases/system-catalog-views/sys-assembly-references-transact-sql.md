---
title: sys. assembly_references (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_references
- sys.assembly_references_TSQL
- assembly_references_TSQL
- sys.assembly_references
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_references catalog view
ms.assetid: 50a5ed42-2d5b-4a11-a0d2-9a02241b078d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5cfd8202754872f73e4462d43adaaba27b4b7386
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880044"
---
# <a name="sysassembly_references-transact-sql"></a>sys.assembly_references(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  하나가 다른 하나를 직접 참조하는 각 쌍의 어셈블리당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|이 참조가 속한 어셈블리의 ID입니다.|  
|**referenced_assembly_id**|**int**|참조되는 어셈블리의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;CLR 어셈블리 카탈로그 뷰](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
