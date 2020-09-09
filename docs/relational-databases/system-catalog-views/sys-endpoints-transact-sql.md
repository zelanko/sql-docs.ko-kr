---
description: sys.endpoints(Transact-SQL)
title: sys. 엔드포인트 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73555ee11e3f03c8478ca170039b7b367036fc4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548762"
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  시스템에서 만든 각 엔드포인트에 대해 한 행을 포함합니다. SYSTEM 엔드포인트는 항상 하나만 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|엔드포인트의 이름입니다. 서버 내에서 고유합니다. Null을 허용하지 않습니다.|  
|**endpoint_id**|**int**|엔드포인트의 ID입니다. 서버 내에서 고유합니다. ID가 65536보다 작은 엔드포인트는 시스템 엔드포인트입니다. Null을 허용하지 않습니다.|  
|**principal_id**|**int**|이 엔드포인트를 만들고 소유하는 서버 보안 주체의 ID입니다. Null을 허용합니다.|  
|**protocol**|**tinyint**|엔드포인트 프로토콜입니다.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = 명명된 파이프<br /><br /> 4 = 공유 메모리<br /><br /> 5 = VIA(Virtual Interface Adapter)<br /><br /> Null을 허용하지 않습니다.|  
|**protocol_desc**|**nvarchar(60)**|엔드포인트 프로토콜에 대한 설명입니다. NULL을 허용합니다. 다음 값 중 하나입니다.<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **VIA** 참고: VIA 프로토콜은 더 이상 사용 되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**type**|**tinyint**|엔드포인트 페이로드 유형입니다.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> Null을 허용하지 않습니다.|  
|**type_desc**|**nvarchar(60)**|엔드포인트 페이로드 유형에 대한 설명입니다. Null을 허용합니다. 다음 값 중 하나입니다.<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**상태**|**tinyint**|엔드포인트 상태입니다.<br /><br /> 0 = STARTED, 요청을 수신 대기 및 처리 중입니다.<br /><br /> 1 = STOPPED, 요청을 수신 대기 중이지만 처리하고 있지 않습니다.<br /><br /> 2 = DISABLED, 수신 대기하지 않습니다.<br /><br /> 기본 상태는 1입니다. Null을 허용합니다.|  
|**state_desc**|**nvarchar(60)**|엔드포인트 상태에 대한 설명입니다.<br /><br /> STARTED = 요청을 수신 대기 및 처리 중입니다.<br /><br /> STOPPED = 요청을 수신 대기 중이지만 처리하고 있지 않습니다.<br /><br /> DISABLED = 수신 대기하지 않습니다.<br /><br /> 기본 상태는 STOPPED입니다.<br /><br /> Null을 허용합니다.|  
|**is_admin_endpoint**|**bit**|엔드포인트가 관리자용인지 여부를 나타냅니다.<br /><br /> 0 = 비관리 엔드포인트입니다.<br /><br /> 1 = 엔드포인트가 관리 엔드포인트입니다.<br /><br /> Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
