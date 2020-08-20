---
description: dbo.systargetservers(Transact-SQL)
title: dbo.systargetservers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9b8391e01d681f50f36a6f0c5b1b13a2726eaae5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488948"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  해당 다중 서버 작업 도메인에 현재 참여하는 대상 서버를 기록합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|서버 ID입니다.|  
|**server_name**|**sysname**|서버 이름입니다.|  
|**location**|**nvarchar(200)**|지정된 대상 서버의 위치입니다.|  
|**time_zone_adjustment**|**int**|GMT(그리니치 표준시)를 적용한 시간 조정 간격(시)입니다.|  
|**enlist_date**|**datetime**|지정한 대상 서버가 참여한 날짜와 시간입니다.|  
|**last_poll_date**|**datetime**|지정 된 대상 서버가 실행할 작업에 대 한 다중 서버 **sysdownloadlist** 시스템 테이블을 마지막으로 폴링한 날짜와 시간입니다.|  
|**status**|**int**|대상 서버의 상태입니다.<br /><br /> **1** = 보통<br /><br /> **2** = 다시 동기화 보류 중<br /><br /> **4** = 오프 라인 상태로 의심 됨|  
|**local_time_at_last_poll**|**datetime**|작업 운영에 대해 대상 서버가 마지막으로 폴링된 날짜와 시간입니다.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|대상 서버에서 **sp_msx_enlist** 를 실행 하는 사용자의 사용자 이름입니다.|  
|**poll_internal**|**int**|대상 서버가 새 다운로드 명령에 대해 마스터 서버를 폴링하기 전의 경과 시간(초)을 표시한 것입니다.|  
  
  
