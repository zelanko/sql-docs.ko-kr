---
title: dbo.systargetservers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f425fb530d10abb4a3285f664b8bed8b083197b8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260709"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  해당 다중 서버 작업 도메인에 현재 참여하는 대상 서버를 기록합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|서버 ID입니다.|  
|**server_name**|**sysname**|서버 이름입니다.|  
|**location**|**nvarchar(200)**|지정된 대상 서버의 위치입니다.|  
|**time_zone_adjustment**|**int**|GMT(그리니치 표준시)를 적용한 시간 조정 간격(시)입니다.|  
|**enlist_date**|**datetime**|지정한 대상 서버가 참여한 날짜와 시간입니다.|  
|**last_poll_date**|**datetime**|날짜 및 시간을 지정 된 대상 서버가 다중 서버의 마지막으로 폴링한 **sysdownloadlist** 작업을 실행 하려면 시스템 테이블입니다.|  
|**상태**|**int**|대상 서버의 상태입니다.<br /><br /> **1** = 정상<br /><br /> **2** = 다시 동기화 보류 중<br /><br /> **4** = 오프 라인 상태로 의심 됨|  
|**local_time_at_last_poll**|**datetime**|작업 운영에 대해 대상 서버가 마지막으로 폴링된 날짜와 시간입니다.|  
|**enlisted_by_nt_user**|**nvarchar(100)**|실행 하는 사용자의 사용자 이름 **sp_msx_enlist** 대상 서버에 있습니다.|  
|**poll_internal**|**int**|대상 서버가 새 다운로드 명령에 대해 마스터 서버를 폴링하기 전의 경과 시간(초)을 표시한 것입니다.|  
  
  
