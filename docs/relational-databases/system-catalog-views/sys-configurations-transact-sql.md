---
description: sys.configurations(Transact-SQL)
title: sys.configurations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b041e0bb17e0c290225ecb951fe26d95ab07770
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486461"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  시스템에 서버 차원의 구성 옵션 값마다 한 행을 포함합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|구성 값에 대한 고유한 ID입니다.|  
|**name**|**nvarchar(35)**|구성 옵션의 이름입니다.|  
|**value**|**sql_variant**|이 옵션에 구성된 값입니다.|  
|**minimum**|**sql_variant**|구성 옵션의 최소값입니다.|  
|**maximum**|**sql_variant**|구성 옵션의 최대값입니다.|  
|**value_in_use**|**sql_variant**|이 옵션에 대해 현재 유효한 값을 실행하고 있습니다.|  
|**description**|**nvarchar(255)**|구성 옵션의 설명입니다.|  
|**is_dynamic**|**bit**|1 = RECONFIGURE 문이 실행될 때 효력을 갖는 변수입니다.|  
|**is_advanced**|**bit**|1 = **show advancedoption** 가 설정 된 경우에만 변수가 표시 됩니다.|  
  
 ## <a name="remarks"></a>설명
  모든 서버 구성 옵션 목록은 [서버 구성 옵션 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)를 참조 하세요.  
  
> [!NOTE]  
>  데이터베이스 수준 구성 옵션은 [ALTER DATABASE 범위 구성 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)를 참조 하세요. 소프트 NUMA를 구성 하려면 [소프트 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)를 참조 하세요.  
 
sys.configurations 카탈로그 뷰를 사용 하 여 config_value (값 열), run_value (value_in_use 열) 및 구성 옵션이 동적 인지 여부 (서버 엔진을 다시 시작 하거나 is_dynamic 열을 요구 하지 않음)를 확인할 수 있습니다.

> [!NOTE]
> Sp_configure 결과 집합의 config_value **sys.configurations** 열과 같습니다. **Run_value** 은 **sys.configurations. value_in_use** 열과 동일 합니다.

다음 쿼리를 사용 하 여 구성 된 값이 설치 되지 않은 경우를 확인할 수 있습니다.

```SQL
select * from sys.configurations where value != value_in_use
```

값이 구성 옵션에 대 한 변경 값과 동일 하지만 **value_in_use** 동일 하지 않은 경우 RECONFIGURE 명령이 실행 되지 않았거나 실패 했거나 서버 엔진을 다시 시작 해야 합니다.

값과 value_in_use 동일 하지 않을 수 있는 구성 옵션이 있으며이는 예상 된 동작입니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

"max server memory (MB)"-기본 구성 값 0은 value_in_use = 2147483647 "min server memory (MB)"로 표시 됩니다. 기본 구성 된 값 0은 value_in_use = 8 (32 비트) 또는 16 (64 비트)으로 표시 될 수 있습니다. 

경우에 따라 **value_in_use** 0이 됩니다. 이 경우 "true" **value_in_use** 8 (32 비트) 또는 16 (64 비트)입니다.

**Is_dynamic** 열은 구성 옵션의 다시 시작이 필요한 지 여부를 확인 하는 데 사용할 수 있습니다. is_dynamic = 1은 다시 구성 (T-sql)이 실행 될 때 새 값이 "즉시" 적용 됨을 의미 합니다. 경우에 따라 서버 엔진은 새 값을 즉시 계산 하지 않을 수 있지만이 작업은 일반적인 실행 과정에서 수행 됩니다. is_dynamic = 0은 다시 구성 (T-sql) 명령이 실행 된 경우에도 서버를 다시 시작할 때까지 변경 된 구성 값이 적용 되지 않음을 의미 합니다.

동적이 아닌 구성 옵션의 경우에는 구성 변경 내용을 설치 하는 첫 번째 단계를 수행 하기 위해 RECONFIGURE (T-sql) 명령이 실행 되었는지 여부를 확인할 수 있는 방법이 없습니다. SQL Server를 다시 시작 하 여 구성 변경을 설치 하기 전에 RECONFIGURE (T-sql) 명령을 실행 하 여 SQL Server를 다시 시작한 후 모든 구성 변경 내용이 적용 되는지 확인 합니다. 
 
 
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;서버 차원의 구성 카탈로그 뷰 ](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
