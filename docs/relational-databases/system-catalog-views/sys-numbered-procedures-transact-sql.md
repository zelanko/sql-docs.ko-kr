---
description: sys.numbered_procedures(Transact-SQL)
title: sys.numbered_procedures (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 410c7b9a04463aeed0a777bb8c3bfcb75dfc9e32
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97405159"
---
# <a name="sysnumbered_procedures-transact-sql"></a>sys.numbered_procedures(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  번호를 매긴 프로시저로 작성된 각 SQL Server 저장 프로시저당 한 개의 행을 포함합니다. 여기에는 기본(번호 = 1) 저장 프로시저에 대한 행은 표시되지 않습니다. 기본 저장 프로시저에 대 한 항목은 **sys. objects** 및 **sys.debug** 와 같은 뷰에서 찾을 수 있습니다.  
  
> [!IMPORTANT]  
>  번호를 매긴 프로시저는 더 이상 사용되지 않으므로 사용하지 않는 것이 좋습니다. 이 카탈로그 뷰를 사용하는 쿼리가 컴파일되면 DEPRECATION_ANNOUNCEMENT 이벤트가 발생합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|저장 프로시저 개체의 ID입니다.|  
|**procedure_number**|**smallint**|개체 내에서 이 프로시저의 번호이며 2 이상입니다.|  
|**정의**|**nvarchar(max)**|해당 프로시저를 정의하는 SQL Server 텍스트입니다.<br /><br /> NULL = 암호화됨|  
  
> [!NOTE]  
>  번호를 매긴 프로시저에는 XML 및 CLR 매개 변수를 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
