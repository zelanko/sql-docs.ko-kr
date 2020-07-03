---
title: sys. server_triggers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7ce21b1c997a1530212f9a0317632f665c9ef503
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85884463"
---
# <a name="sysserver_triggers-transact-sql"></a>sys.server_triggers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  TR 또는 TA의 object_type이 있는 모든 서버 수준 DDL 트리거의 집합을 포함합니다. CLR 트리거의 경우에는 어셈블리를 **master** 데이터베이스에 로드 해야 합니다. 모든 서버 수준 DDL 트리거 이름은 단일 전역 범위에 존재합니다.  
  
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
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
