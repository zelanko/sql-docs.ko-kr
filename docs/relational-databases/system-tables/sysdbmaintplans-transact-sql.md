---
title: sysdbmaintplans (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs: TSQL
helpviewer_keywords: sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c9e9dd779b6a84f76844d27cef19ae8ff7c7f9d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 테이블에 포함 되어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이전 버전에서 업그레이드 된 인스턴스에 대 한 기존 정보를 유지 하기 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 테이블의 내용을 변경하지 않습니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획 ID입니다.|  
|**plan_name**|**sysname**|데이터베이스 유지 관리 계획 이름입니다.|  
|**date_created**|**datetime**|데이터베이스 유지 관리 계획을 만든 날짜입니다.|  
|**소유자**|**sysname**|데이터베이스 유지 관리 계획의 소유자입니다.|  
|**max_history_rows**|**int**|시스템 테이블에 있는 데이터베이스 유지 관리 계획을 기록하는 데 사용하도록 지정된 최대 행 수입니다.|  
|**remote_history_server**|**sysname**|기록 보고서를 작성할 원격 서버의 이름입니다.|  
|**max_remote_history_rows**|**int**|기록 보고서를 작성할 수 있는 원격 서버의 시스템 테이블에서 지정된 최대 행 수입니다.|  
|**user_defined_1**|**int**|기본값은 NULL입니다.|  
|**user_defined_2**|**nvarchar (100)**|기본값은 NULL입니다.|  
|**user_defined_3**|**datetime**|기본값은 NULL입니다.|  
|**user_defined_4**|**uniqueidentifier**|기본값은 NULL입니다.|  
|**log_shipping**|**bit**|로그 전달 상태입니다.<br /><br /> **0** = 사용 안 함 **1** = 사용|  
  
  
