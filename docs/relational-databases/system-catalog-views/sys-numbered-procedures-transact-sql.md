---
title: sys.numbered_procedures (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6a8dbd0f26b39c4fda367d2057cb9eb361586c5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysnumberedprocedures-transact-sql"></a>sys.numbered_procedures(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  번호를 매긴 프로시저로 작성된 각 SQL Server 저장 프로시저당 한 개의 행을 포함합니다. 여기에는 기본(번호 = 1) 저장 프로시저에 대한 행은 표시되지 않습니다. 기본 저장된 프로시저에 대 한 항목 보기에서와 같은 확인할 수 있습니다 **sys.objects** 및 **sys.procedures**합니다.  
  
> [!IMPORTANT]  
>  번호를 매긴 프로시저는 더 이상 사용되지 않으므로 사용하지 않는 것이 좋습니다. 이 카탈로그 뷰를 사용하는 쿼리가 컴파일되면 DEPRECATION_ANNOUNCEMENT 이벤트가 발생합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|저장 프로시저 개체의 ID입니다.|  
|**procedure_number**|**smallint**|개체 내에서 이 프로시저의 번호이며 2 이상입니다.|  
|**정의**|**nvarchar(max)**|해당 프로시저를 정의하는 SQL Server 텍스트입니다.<br /><br /> NULL = 암호화됨|  
  
> [!NOTE]  
>  번호를 매긴 프로시저에는 XML 및 CLR 매개 변수를 사용할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
