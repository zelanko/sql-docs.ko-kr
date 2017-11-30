---
title: sys.backup_devices (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dab6ab1eedc6ae0e6a7af91fbad65a8ed36562a1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sysbackupdevices-transact-sql"></a>sys.backup_devices(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용 하 여 등록 된 각 백업 장치에 대 한 행을 포함 **sp_addumpdevice** 또는에서 만든 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|백업 장치의 이름입니다. 세트에서 고유합니다.|  
|**유형**|**tinyint**|백업 장치의 유형입니다.<br /><br /> 2 = 디스크<br /><br /> 3 = 디스켓(사용되지 않음)<br /><br /> 5 = 테이프<br /><br /> 6 = 파이프(사용되지 않음)<br /><br /> 7 = 가상 장치(타사 백업 공급업체에서 선택적으로 사용)<br /><br /> 일반적으로 디스크(2)와 테이프(5)만 사용됩니다.|  
|**type_desc**|**nvarchar (60)**|백업 장치 유형에 대한 설명입니다.<br /><br /> DISK<br /><br /> DISKETTE(사용되지 않음)<br /><br /> TAPE<br /><br /> PIPE(사용되지 않음)<br /><br /> VIRTUAL_DEVICE(타사 백업 공급업체에서 선택적으로 사용)<br /><br /> 일반적으로 DISK와 TAPE만 사용됩니다.|  
|**physical_name**|**nvarchar (260)**|백업 장치의 물리적 파일 이름 또는 경로입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
