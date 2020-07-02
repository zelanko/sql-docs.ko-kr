---
title: backupmediaset (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86f1b7fcc8e801f70bf070911feadb059108dff5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750363"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  각 백업 미디어 세트에 대해 한 행을 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|고유한 미디어 세트 ID 번호입니다. ID, 즉 기본 키입니다.|  
|**media_uuid**|**uniqueidentifier**|미디어 세트의 UUID입니다. 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 미디어 세트에는 UUID가 있습니다.<br /><br /> 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 미디어 세트에 미디어 패밀리가 하나만 포함 되어 있으면 **media_uuid** 열이 NULL 일 수 있습니다 (**media_family_count** 1).|  
|**media_family_count**|**tinyint**|미디어 세트에서 미디어 패밀리의 번호입니다. NULL일 수 있습니다.|  
|**name**|**nvarchar(128)**|미디어 세트의 이름입니다. NULL일 수 있습니다.<br /><br /> 자세한 내용은 MEDIANAME and MEDIADESCRIPTION in [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조 하세요.|  
|**한**|**nvarchar(255)**|미디어 세트의 문자 설명입니다. NULL일 수 있습니다.<br /><br /> 자세한 내용은 MEDIANAME and MEDIADESCRIPTION in [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조 하세요.|  
|**software_name**|**nvarchar(128)**|미디어 레이블을 기록한 백업 소프트웨어의 이름입니다. NULL일 수 있습니다.|  
|**software_vendor_id**|**int**|백업 미디어 레이블을 기록한 소프트웨어 공급업체의 ID 번호입니다. NULL일 수 있습니다.<br /><br /> 의 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 16 진수 0x1200입니다.|  
|**MTF_major_version**|**tinyint**|이 미디어 세트를 생성하는 데 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format의 주 버전 번호입니다. NULL일 수 있습니다.|  
|**mirror_count**|**tinyint**|미디어 세트에 있는 미러 수입니다.|  
|**is_password_protected**|**bit**|미디어 세트의 암호 보호 여부입니다.<br /><br /> 0 = 보호되지 않음<br /><br /> 1 = 보호됨|  
|**is_compressed**|**bit**|백업의 압축 여부:<br /><br /> 0 = 압축되지 않음<br /><br /> 1 = 압축됨<br /><br /> **Msdb** 를 업그레이드 하는 동안이 값은 NULL로 설정 됩니다. 백업이 압축되지 않았음을 나타냅니다.|  
|**is_encrypted**|**조금**|백업의 암호화 여부입니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨|  
  
## <a name="remarks"></a>설명  
 LOADHISTORY를 사용 하는 *backup_device* 에서만 RESTORE verifyonly는 **backupmediaset** 테이블의 열을 미디어 세트 헤더의 적절 한 값으로 채웁니다.  
  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
