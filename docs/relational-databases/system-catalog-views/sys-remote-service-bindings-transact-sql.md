---
title: sys. remote_service_bindings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 45e2050a08ce52ba915c0670a4da26a4517a1a3c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787089"
---
# <a name="sysremote_service_bindings-transact-sql"></a>sys.remote_service_bindings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  이 카탈로그 뷰에는 각 원격 서비스 바인딩에 대한 행이 포함되어 있습니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|이 원격 서비스 바인딩의 이름입니다. NULL을 허용하지 않습니다.|  
|**remote_service_binding_id**|**int**|이 원격 서비스 바인딩의 ID입니다. NULL을 허용하지 않습니다.|  
|**principal_id**|**int**|이 원격 서비스 바인딩을 소유한 데이터베이스 보안 주체의 ID입니다. NULL을 허용합니다.|  
|**remote_service_name**|**nvarchar(256)**|이 바인딩이 적용되는 원격 서비스의 이름입니다. NULL을 허용합니다.|  
|**service_contract_id**|**int**|이 바인딩이 적용되는 계약의 ID입니다. 값 0은 이 바인딩이 서비스의 모든 계약에 적용됨을 의미하는 와일드카드입니다. NULL을 허용하지 않습니다.|  
|**remote_principal_id**|**int**|원격 서비스 바인딩에 지정된 사용자의 ID입니다. Service Broker는 지정된 계약에서 지정된 서비스와 통신할 때 이 사용자가 소유한 인증서를 사용합니다. NULL을 허용합니다.|  
|**is_anonymous_on**|**bit**|이 원격 서비스 바인딩은 ANONYMOUS 보안을 사용합니다. 대화를 시작하는 사용자의 ID는 대상 서비스에 제공되지 않습니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
