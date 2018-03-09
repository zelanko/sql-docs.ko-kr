---
title: RESTORE LABELONLY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5cbf694abdf86a5e5e13f2799f5b1f4b808a498
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---labelonly-transact-sql"></a>RESTORE 문-LABELONLY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 백업 장치로 식별하는 백업 미디어에 대한 정보가 포함된 결과 집합을 반환합니다.  
  
> [!NOTE]  
>  인수 설명에 대 한 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>인수  
 RESTORE LABELONLY 인수 설명에 대 한 참조 [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>결과 집합  
 RESTORE LABELONLY의 결과 집합은 다음 정보를 가진 단일 행으로 구성됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**MediaName**|**nvarchar(128)**|미디어의 이름입니다.|  
|**MediaSetId**|**uniqueidentifier**|미디어 세트의 고유 ID입니다.|  
|**FamilyCount**|**int**|미디어 세트에서 미디어 패밀리의 번호입니다.|  
|**FamilySequenceNumber**|**int**|해당 패밀리의 시퀀스 번호입니다.|  
|**MediaFamilyId**|**uniqueidentifier**|미디어 패밀리의 고유 ID입니다.|  
|**MediaSequenceNumber**|**int**|미디어 패밀리에 있는 해당 미디어의 시퀀스 번호입니다.|  
|**MediaLabelPresent**|**tinyint**|미디어 설명에 다음이 포함되는지 여부입니다.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] tape Format 미디어 레이블<br /><br /> **0** = 미디어 설명|  
|**MediaDescription**|**nvarchar(255)**|자유 형식 텍스트로 된 미디어 설명 또는 Tape Format 미디어 레이블입니다.|  
|**SoftwareName**|**nvarchar(128)**|미디어 레이블을 기록하는 백업 소프트웨어의 이름입니다.|  
|**SoftwareVendorId**|**int**|백업을 기록하는 소프트웨어 공급업체의 고유 공급업체 ID입니다.|  
|**MediaDate**|**datetime**|레이블을 작성한 날짜와 시간입니다.|  
|**Mirror_Count**|**int**|세트에 있는 미러 수(1-4)입니다.<br /><br /> 참고: 집합에 있는 다른 미러에 대해 기록 된 레이블은 동일 합니다.|  
|**IsCompressed**|**bit**|백업의 압축 여부:<br /><br /> 0 = 압축되지 않음<br /><br /> 1 = 압축됨|  
  
> [!NOTE]  
>  미디어 세트에 대한 암호를 정의한 경우 RESTORE LABELONLY는 올바른 미디어 암호를 명령의 MEDIAPASSWORD 옵션에 지정한 경우에만 정보를 반환합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 백업 미디어의 내용을 빨리 찾을 수 있는 방법은 RESTORE LABELONLY를 실행하는 것입니다. RESTORE LABELONLY에서는 미디어 헤더만 읽기 때문에 고성능의 테이프 장치를 사용하는 경우에도 이 문은 빨리 완료됩니다.  
  
## <a name="security"></a>보안  
 백업 작업에서는 미디어 세트에 선택적으로 암호를 지정할 수 있습니다. 미디어 세트에 암호가 정의되어 있는 경우에는 RESTORE 문에서 정확한 암호를 지정해야 합니다. 암호 무단으로 복원 작업을 수행할 수과 무단으로 사용 하 여 미디어에 사용할 백업 세트 추가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구입니다. 하지만 암호를 사용해도 BACKUP 문의 FORMAT 옵션을 사용하여 미디어를 덮어쓰는 작업은 수행됩니다.  
  
> [!IMPORTANT]  
>  이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]백업을 보호 하는 것에 대 한 백업 테이프를 저장 하 여 안전한 위치에 또는 디스크 파일에 적절 한 액세스 제어 목록 (Acl)로 보호 되는 백업 하는 것이 좋습니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.  
  
### <a name="permissions"></a>Permissions  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 백업 세트나 백업 장치에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
