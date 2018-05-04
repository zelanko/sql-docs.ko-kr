---
title: sysreplicationalerts (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d3b1b7c1950f76d931910890b5950eea39addbcd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제 경고를 발생시키는 조건에 대한 정보를 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|경고의 ID입니다.|  
|**상태**|**int**|사용자 정의 값입니다.<br /><br /> **0** = 서비스 안 됨.<br /><br /> **1** = 서비스를 제공 합니다.|  
|**agent_type**|**int**|에이전트의 유형입니다.<br /><br /> **1** = 스냅숏 에이전트입니다.<br /><br /> **2** = 로그 판독기 에이전트입니다.<br /><br /> **3** = 배포 에이전트입니다.<br /><br /> **4** = 병합 에이전트입니다.|  
|**agent_id**|**int**|테이블에서 에이전트 ID **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**, 또는 **MSmerge_agents**합니다.|  
|**error_id**|**int**|에 저장 된 오류의 ID **MSrepl_errors**합니다.|  
|**alert_error_code**|**int**|해당 레코드를 기록할 때 발생하는 경고의 메시지 ID입니다.|  
|**time**|**datetime**|레코드가 삽입된 시각입니다.|  
|**publisher**|**sysname**|현재 경고를 발생시킨 에이전트와 관련된 게시자의 이름입니다.|  
|**publisher_db**|**sysname**|현재 경고를 발생시킨 에이전트와 관련된 게시자 데이터베이스입니다.|  
|**게시**|**sysname**|현재 경고를 발생시킨 에이전트와 관련된 게시입니다.|  
|**publication_type**|**int**|게시의 유형입니다.<br /><br /> **0** = 스냅숏 합니다.<br /><br /> **1** = 트랜잭션.<br /><br /> **2** = 병합 합니다.|  
|**subscriber**|**sysname**|이 경고를 발생시킨 에이전트와 관련된 구독자의 이름입니다.|  
|**subscriber_db**|**sysname**|이 경고를 발생시킨 에이전트와 관련된 구독자 데이터베이스 이름입니다.|  
|**article**|**sysname**|이 경고를 발생시킨 에이전트와 관련된 아티클의 이름입니다.|  
|**destination_object**|**sysname**|이 경고와 관련된 구독 테이블의 이름입니다.|  
|**source_object**|**sysname**|이 경고와 관련된 게시된 테이블의 이름입니다.|  
|**alert_error_text**|**ntext**|경고의 텍스트입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
