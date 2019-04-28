---
title: sys.syscurconfigs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3ef0f49229ab374a0ca9e2dce12d7fa6ea5f59bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62693839"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 구성 옵션 각각에 대한 항목을 포함합니다. 또한 이 뷰에는 구성 구조를 설명하는 네 개의 항목이 포함되어 있습니다. **syscurconfigs** 사용자가 쿼리할 때 동적으로 작성 됩니다. 자세한 내용은 [sys.sysconfigures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md)합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**value**|**int**|사용자 수정이 가능한 변수 값입니다. RECONFIGURE가 실행된 경우에만 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 사용합니다.|  
|**config**|**smallint**|구성 변수 번호입니다.|  
|**comment**|**nvarchar(255)**|구성 옵션에 대한 설명입니다.|  
|**상태**|**smallint**|옵션의 상태를 표시하는 비트맵입니다. 가능한 값은 다음과 같습니다.<br /><br /> 0 = 정적. 서버가 다시 시작될 때 설정이 적용됩니다.<br /><br /> 1 = 동적. RECONFIGURE 문이 실행될 때 변수가 적용됩니다.<br /><br /> 2 = 고급. 변수가 표시 됩니다 경우에만 합니다 **고급 옵션 표시** 설정 됩니다.<br /><br /> 3 = 동적 및 고급입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
