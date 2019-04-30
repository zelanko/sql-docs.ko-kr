---
title: sys.database_scoped_configurations (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af6c2996877f4ab7d8a2305c4f6fe4b30a0127cc
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473749"
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  구성 별로 하나의 행을 포함 합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|구성 옵션의 ID입니다.|  
|**name**|**nvarchar(60)**|구성 옵션의 이름입니다. 가능한 구성에 대 한 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)합니다.|  
|**value**|**sqlvariant**|주 복제본이 구성 옵션에 대 한 설정 값입니다.|  
|**value_for_secondary**|**sqlvariant**|보조 복제본에 대 한이 구성 옵션에 대 한 설정 값입니다.|  
|**is_value_default**|**bit** |값 집합이 기본 값인지 여부를 지정 합니다.|
  
##  <a name="Permissions"></a> Permissions  
**public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
NULL 값으로 반환 될 때 **value_for_secondary**, 즉, 주 지역에 보조 복제본 설정 되어 있는지 합니다.  
 
데이터베이스 범위 구성 설정은 데이터베이스와 함께 전달됩니다. 즉, 지정된 데이터베이스가 복원 또는 연결되는 경우 기존 구성 설정이 유지됩니다.
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
