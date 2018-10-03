---
title: sys.sysmembers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysmembers_TSQL
- sysmembers
- sys.sysmembers
- sysmembers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmembers system table
- sys.sysmembers compatibility view
ms.assetid: ceb18341-f985-4849-ac83-21d67ab7b980
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5672c6b027e001e2aaf2a344c2710d2a28e62e9e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689761"
---
# <a name="syssysmembers-transact-sql"></a>sys.sysmembers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 역할의 각 멤버에 대해 한 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**memberuid**|**smallint**|역할 멤버의 사용자 ID입니다. 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
|**groupuid**|**smallint**|역할의 사용자 ID입니다. 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
