---
title: sys.server_triggers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_triggers
- sys.server_triggers_TSQL
- server_triggers_TSQL
- sys.server_triggers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_triggers catalog view
ms.assetid: 25926ff4-9271-45bf-bc32-d5d3344bd47a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b497487cbad0718d0cbaca30a7e88e7fb78562ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysservertriggers-transact-sql"></a>sys.server_triggers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  TR 또는 TA의 object_type이 있는 모든 서버 수준 DDL 트리거의 집합을 포함합니다. CLR 트리거의 경우 어셈블리에 로드 해야는 **마스터** 데이터베이스입니다. 모든 서버 수준 DDL 트리거 이름은 단일 전역 범위에 존재합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|트리거의 이름입니다.|  
|**object_id**|**int**|개체의 ID입니다.|  
|**parent_class**|**tinyint**|부모 클래스입니다. 항상 다음과 같습니다.<br /><br /> 100 = 서버|  
|**parent_class_desc**|**nvarchar(60)**|부모 클래스에 대한 설명입니다. 항상 다음과 같습니다.<br /><br /> SERVER|  
|**parent_id**|**int**|SERVER 상의 트리거에 대해 항상 0입니다.|  
|**type**|**char(2)**|개체 유형:<br /><br /> TA = 어셈블리(CLR) 트리거<br /><br /> TR = SQL 트리거|  
|**type_desc**|**nvarchar(60)**|개체 유형의 클래스에 대한 설명입니다.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|트리거를 만든 날짜입니다.|  
|**modify_date**|**datetime**|ALTER 문을 사용하여 마지막으로 트리거를 수정한 날짜입니다.|  
|**is_ms_shipped**|**bit**|내부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 사용자 대신 만든 트리거입니다.|  
|**is_disabled**|**bit**|1 = 트리거가 비활성화됩니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
