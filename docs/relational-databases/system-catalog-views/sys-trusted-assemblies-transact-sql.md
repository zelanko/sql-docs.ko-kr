---
title: sys.trusted_assemblies (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/14/2017
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
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: 
caps.latest.revision: 
author: tmullaney
ms.author: thmullan
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71d13ae733551a3c475176343250f9ee671756f3
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

서버에 대 한 신뢰할 수 있는 각 어셈블리에 대해 한 행을 포함 합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|열 이름 |데이터 형식 |Description |
|--- |--- |--- |
|해시 |varbinary(8000) |어셈블리 콘텐츠 SHA2_512 해시입니다. |
|description |nvarchar(4000) |선택적 사용자 정의 설명의 어셈블리입니다. 단순한 이름, 버전 번호, culture, 공개 키 및 신뢰 어셈블리의 아키텍처 등을 인코딩하는 정식 이름을 사용 하는 것이 좋습니다. 이 값은 고유 하 게 공용 언어 런타임 (CLR) 변에 어셈블리를 식별 되며 sys.assemblies clr_name 값과 같습니다. |
|create_date |datetime2 |어셈블리는 신뢰할 수 있는 어셈블리의 목록에 추가 된 날짜입니다. |
|created_by |nvarchar(128) |로그인 이름 목록에 어셈블리를 추가 하는 보안 주체입니다. |
| | | |


## <a name="remarks"></a>주의  

사용 하 여 **sp_add_trusted_assembly 추가 해야 할** 및 **sys.trusted_assemblies 추가 해야 할** 에서 어셈블리 추가 또는 제거 `sys.trusted_assemblies`합니다.

## <a name="see-also"></a>관련 항목:  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

