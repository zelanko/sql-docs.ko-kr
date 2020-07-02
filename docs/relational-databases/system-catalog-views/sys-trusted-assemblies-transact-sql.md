---
title: sys. trusted_assemblies (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
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
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8144e6a134edf3331b34f5c91f6d676e6a9302f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733398"
---
# <a name="systrusted_assemblies-transact-sql"></a>sys.trusted_assemblies(Transact-SQL)  
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

서버에 대해 신뢰할 수 있는 각 어셈블리에 대 한 행을 포함 합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|열 이름 |데이터 형식 |Description |
|--- |--- |--- |
|hash |varbinary(8000) |어셈블리 콘텐츠의 해시를 SHA2_512 합니다. |
|description |nvarchar(4000) |어셈블리에 대 한 선택적 사용자 정의 설명입니다. 신뢰할 수 있는 어셈블리의 단순한 이름, 버전 번호, 문화권, 공개 키 및 아키텍처를 인코딩하는 정식 이름을 사용 하는 것이 좋습니다. 이 값은 CLR (공용 언어 런타임) 쪽에서 어셈블리를 고유 하 게 식별 하며,이 값은 sys. 어셈블리의 clr_name 값과 동일 합니다. |
|create_date |datetime2 |어셈블리가 신뢰할 수 있는 어셈블리 목록에 추가 된 날짜입니다. |
|created_by |nvarchar(128) |목록에 어셈블리를 추가한 사용자의 로그인 이름입니다. |
| | | |


## <a name="remarks"></a>설명  

**Sp_add_trusted_assembly를 추가 하** 고 trusted_assemblies를 추가 **해야** 합니다 .를 사용 하 여에서 어셈블리를 추가 하거나 제거 `sys.trusted_assemblies` 합니다.

## <a name="see-also"></a>참고 항목  
  [sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys. sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [drop assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

