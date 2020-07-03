---
title: sysopentapes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2e789796cd504404ad4f71d95c66815498b1a04
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881314"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 열려 있는 각 테이프 디바이스에 대해 한 행을 포함합니다. 이 뷰는 **master** 데이터베이스에 저장 됩니다.  
  
> [!IMPORTANT]  
>  이 시스템 테이블은 이전 버전과의 호환성을 위해 뷰로 포함됩니다. 대신 [dm_io_backup_tapes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 동적 관리 뷰를 사용 합니다.  
  
> [!NOTE]  
>  **Sysopentapes** 뷰를 삭제할 수 없습니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64)**|열려 있는 테이프 디바이스의 물리적 파일 이름입니다. 테이프 장치를 열고 해제 하는 방법에 대 한 자세한 내용은 [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) 및 [RESTORE &#40;transact-sql&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조 하세요.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
  
