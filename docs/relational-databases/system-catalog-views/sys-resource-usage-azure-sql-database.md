---
title: resource_usage (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 3be4ff07923759af53b929852d4dbaa4088a77f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904429"
---
# <a name="sysresource_usage-azure-sql-database"></a>sys.resource_usage(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]
>  이 기능은 미리 보기 상태입니다. 이 기능은 향후 릴리스에서 변경되거나 제거될 수 있으므로 이 기능의 특정 구현에 의존하지 마세요.  
> 
>  미리 보기 상태에 있는 동안 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 작업 팀에서 이 DMV에 대해 데이터 컬렉션을 설정 및 해제할 수 있음:  
> 
>  -   설정된 경우 집계 시 DMV에서 현재 데이터를 반환합니다.  
> -   해제된 경우DMV에서 기록 데이터를 반환하며, 이 데이터는 유효하지 않을 수 있습니다.  
  
 현재 서버에서 사용자 데이터베이스에 대한 리소스 사용량 현황 데이터의 시간별 요약을 제공합니다. 기록 데이터는 90일 동안 유지됩니다.  
  
 각 사용자 데이터베이스에 대해 한 시간에 한 개의 행이 지속적으로 있습니다. 해당 시간 동안 데이터베이스가 유휴 상태인 경우라도 행이 있으며 해당 데이터베이스의 usage_in_seconds 값이 0이 됩니다. 스토리지 사용량 및 SKU 정보는 해당 시간에 대해 적절하게 롤업됩니다.  
  
|열|데이터 형식|설명|  
|-------------|---------------|-----------------|  
|time|**datetime**|시간 단위로 시간(UTC)입니다.|  
|database_name|**nvarchar**|사용자 데이터베이스 이름입니다.|  
|sku|**nvarchar**|SKU 이름입니다. 가능한 값은 다음과 같습니다.<br /><br /> 웹<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|해당 시간에 사용된 CPU 시간의 합계입니다.<br /><br /> 참고:이 열은 V11에 대해 사용 되지 않으며 V12에는 적용 되지 않습니다. **값은 항상 0으로 설정 됩니다.**|  
|storage_in_megabytes|**decimal**|데이터베이스 데이터, 인덱스, 저장 프로시저 및 메타데이터를 포함하여 해당 시간에 대한 최대 스토리지 크기입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 보기는 가상 **master** 데이터베이스에 연결할 수 있는 권한이 있는 모든 사용자 역할에 사용할 수 있습니다.  
  
  
