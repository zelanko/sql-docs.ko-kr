---
title: sysopentapes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ea0a8053d0f88a746349010f6b237ae7189b297
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 열려 있는 각 테이프 장치에 대해 한 행을 포함합니다. 이 보기에 저장 되는 **마스터** 데이터베이스입니다.  
  
> [!IMPORTANT]  
>  이 시스템 테이블은 이전 버전과의 호환성을 위해 뷰로 포함됩니다. 대신를 사용 하 여는 [sys.dm_io_backup_tapes &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 동적 관리 뷰.  
  
> [!NOTE]  
>  삭제할 수 없습니다는 **sysopentapes** 보기.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|열려 있는 테이프 장치의 물리적 파일 이름입니다. 열기 및 테이프 장치를 해제 하는 방법에 대 한 자세한 내용은 참조 [백업 &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md) 및 [복원 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)합니다.|  
  
## <a name="permissions"></a>Permissions  
 서버에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
  
