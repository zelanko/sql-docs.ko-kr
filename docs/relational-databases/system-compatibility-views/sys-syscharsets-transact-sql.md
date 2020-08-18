---
description: sys.syscharsets(Transact-SQL)
title: sys.sys문자 집합 (transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47e839f090a3a7420a3da01cb4d468d3da667314
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88399699"
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 사용하기 위해 정의된 각 문자 집합 및 정렬 순서마다 한 행을 포함합니다. 정렬 순서 중 하나가 **sysconfigures** 기본 정렬 순서로 표시 됩니다. 이 정렬 순서만 실제로 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**type**|**smallint**|이 행이 표시하는 엔터티의 유형입니다.<br /><br /> 1001 = 문자 집합<br /><br /> 2001 = 정렬 순서|  
|**id**|**tinyint**|문자 집합 또는 정렬 순서의 고유 ID입니다. 정렬 순서 및 문자 집합은 같은 ID 번호를 공유할 수 없습니다. 1에서 240까지의 ID는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용하도록 예약되어 있습니다.|  
|**csid**|**tinyint**|행이 문자 집합을 표시하는 경우에는 이 필드를 사용하지 않습니다. 행이 정렬 순서를 표시하는 경우에는 정렬 순서가 작성된 기반이 되는 문자 집합의 ID가 이 필드에 사용됩니다. 이 ID를 가진 문자 집합 행은 이 테이블에 있다고 간주됩니다.|  
|**status**|**smallint**|내부 시스템 상태 정보 비트입니다.|  
|**name**|**sysname**|문자 집합 또는 정렬 순서에 대한 고유한 이름입니다. 이 필드에서는 반드시 A-Z 또는 a-z의 문자, 0 - 9의 숫자 및 밑줄(_)만 사용해야 하고 문자로 시작해야 합니다.|  
|**description**|**nvarchar(255)**|문자 집합 또는 정렬 순서의 기능에 관한 선택적 설명입니다.|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**정의**|**image**|문자 집합 또는 정렬 순서의 내부 정의입니다. 이 필드의 데이터 구조는 유형에 따라 달라집니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
