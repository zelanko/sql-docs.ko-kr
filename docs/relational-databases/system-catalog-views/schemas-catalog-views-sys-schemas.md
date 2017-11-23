---
title: sys.schemas (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs: TSQL
helpviewer_keywords: sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c25648add8882a49964a0838315f42b5c9b61e84
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="schemas-catalog-views---sysschemas"></a>스키마 카탈로그 뷰-sys.schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  각 데이터베이스 스키마당 하나의 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스 스키마는 XML 문서의 콘텐츠 모델을 정의하는 XML 스키마와는 다릅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|스키마의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**schema_id**|**int**|스키마의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**principal_id**|**int**|이 스키마를 소유하는 보안 주체의 ID입니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 스키마 또는 역할을 할 네임 스페이스에서 찾을 수 있는 테이블, 뷰, 프로시저 및 함수 등의 개체에 대 한 컨테이너는 **sys.objects** 카탈로그 뷰에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [스키마 카탈로그 뷰 &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
