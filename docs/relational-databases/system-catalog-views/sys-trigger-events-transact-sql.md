---
title: sys.trigger_events (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc2732797551317a392b0ab55d9ecbeb28d990a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091940"
---
# <a name="systriggerevents-transact-sql"></a>sys.trace_events(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트리거가 실행되는 각 이벤트당 한 개의 행을 포함합니다.  
  
> [!NOTE]  
>  **sys.trigger_events** 이벤트 알림에 적용 되지 않습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**\<Sys.events에서 상속 된 열 >**|해당 사항 없음|상속 된 **object_id**, **형식**, **type_desc** 열에서 [sys.events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md).|  
|**is_first**|**bit**|트리거가 해당 이벤트에 대해 처음 실행되도록 표시됩니다.|  
|**is_last**|**bit**|트리거가 해당 이벤트에 대해 마지막에 실행되도록 표시됩니다.|  
|**event_group_type**|**int**|트리거가 생성되는 이벤트 그룹 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
|**event_group_type_desc**|**nvarchar(60)**|트리거가 생성되는 이벤트 그룹에 대한 설명 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
