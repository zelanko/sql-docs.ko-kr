---
title: sys.configurations (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9eb9ced4e010001f42e106ce8b1903e029f2f1c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109566"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  시스템에 서버 차원의 구성 옵션 값마다 한 행을 포함합니다.  

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|구성 값에 대한 고유한 ID입니다.|  
|**name**|**nvarchar(35)**|구성 옵션의 이름입니다.|  
|**value**|**sql_variant**|이 옵션에 구성된 값입니다.|  
|**minimum**|**sql_variant**|구성 옵션의 최소값입니다.|  
|**maximum**|**sql_variant**|구성 옵션의 최대값입니다.|  
|**value_in_use**|**sql_variant**|이 옵션에 대해 현재 유효한 값을 실행하고 있습니다.|  
|**description**|**nvarchar(255)**|구성 옵션의 설명입니다.|  
|**is_dynamic**|**bit**|1 = RECONFIGURE 문이 실행될 때 효력을 갖는 변수입니다.|  
|**is_advanced**|**bit**|1 = 변수가 표시 됩니다 경우에만 합니다 **advancedoption 표시** 설정 됩니다.|  
  
 모든 서버 구성 옵션 목록을 참조 하세요 [서버 구성 옵션 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)합니다.  
  
> [!NOTE]  
>  데이터베이스 수준 구성 옵션에 대해서 [ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)합니다. 소프트 NUMA를 구성 하려면 참조 [SOFT-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [서버 차원의 구성 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
