---
description: sys.database_scoped_configurations (Transact-sql)
title: sys.database_scoped_configurations (Transact-sql) | Microsoft Docs
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
dev_langs:
- TSQL
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: beb536c39db6dbee3bc2e0855de20282bc994fe4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404729"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys.database_scoped_configurations (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

구성 당 한 개의 행을 포함 합니다. 

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|구성 옵션의 ID입니다.|
|**name**|**nvarchar(60)**|구성 옵션의 이름입니다. 가능한 구성에 대 한 자세한 내용은 [ALTER DATABASE 범위 구성 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조 하세요.|
|**value**|**sqlvariant**|주 복제본에 대 한이 구성 옵션에 설정 된 값입니다.|
|**value_for_secondary**|**sqlvariant**|보조 복제본에 대 한이 구성 옵션에 설정 된 값입니다.|
|**is_value_default**|**bit** |설정 값이 기본값 인지 여부를 지정 합니다.|

## <a name="permissions"></a><a name="Permissions"></a> 권한

**public** 역할의 멤버 자격이 필요합니다.

## <a name="remarks"></a>설명

**Value_for_secondary** 에 대 한 값으로 NULL이 반환 되 면 보조 데이터베이스가 주로 설정 된 것입니다.
 
데이터베이스 범위 구성 설정은 데이터베이스와 함께 전달됩니다. 즉, 지정된 데이터베이스가 복원 또는 연결되는 경우 기존 구성 설정이 유지됩니다.

## <a name="see-also"></a>참고 항목

[데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
