---
title: sp_addumpdevice (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addumpdevice_TSQL
- sp_addumpdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], defining
- sp_addumpdevice
ms.assetid: c2d2ae49-0808-46d8-8444-db69a69d0ec3
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 444dbea29259eca54e815ce49c73df3986db8e11
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spaddumpdevice-transact-sql"></a>sp_addumpdevice(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 백업 장치를 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addumpdevice [ @devtype = ] 'device_type'   
    , [ @logicalname = ] 'logical_name'   
    , [ @physicalname = ] 'physical_name'  
      [ , { [ @cntrltype = ] controller_type |  
          [ @devstatus = ] 'device_status' }  
      ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@devtype=** ] **'***device_type***'**  
 백업 장치의 유형입니다. *device_type* 은 **varchar (20)**이며 기본값은 없고 수는 다음 값 중 하나 여야 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**disk**|백업 장치로서의 하드 디스크 파일입니다.|  
|**tape**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에서 지원되는 테이프 장치입니다.<br /><br /> 참고: 테이프 백업 장치에 대한 지원은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.|  
  
 [  **@logicalname =** ] **'***logical_name***'**  
 BACKUP 및 RESTORE 문에서 사용되는 백업 장치의 논리적 이름입니다. *logical_name* 은 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@physicalname =** ] **'***physical_name***'**  
 백업 장치의 물리적 이름입니다. 물리적 이름은 운영 체제 파일 이름에 적용되는 규칙 또는 네트워크 장치에 적용되는 UNC(Universal Naming Convention)를 따라야 하며 전체 경로를 포함해야 합니다. *physical_name* 은 **nvarchar (260)**, 기본값이 없는 값을 NULL 일 수 없습니다.  
  
 원격 네트워크 위치에서 백업 장치를 만드는 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작된 해당 이름이 원격 컴퓨터에 대해 적절한 쓰기 기능을 갖고 있어야 합니다.  
  
 이 매개 변수가 Windows에 의해 로컬 테이프 장치에 할당 된 실제 이름 이어야 합니다 테이프 장치를 추가 하는 경우 예를 들어  **\\ \\. \TAPE0** 컴퓨터에서 첫 번째 테이프 장치에 대 한 합니다. 테이프 장치는 원격 방식으로는 사용할 수 없으며 반드시 서버 컴퓨터에 연결되어야 합니다. 숫자 또는 알파벳이 아닌 문자를 포함한 이름은 앞뒤로 따옴표를 사용해야 합니다.  
  
> [!NOTE]  
>  이 프로시저에서는 지정한 물리적 이름을 카탈로그에 입력합니다. 장치에 액세스하거나 장치를 만들지는 않습니다.  
  
 [ **@cntrltype =** ] **'***controller_type***'**  
 더 이상 사용되지 않습니다. 지정된 경우 이 매개 변수는 무시됩니다. 이전 버전과의 호환성을 위해서만 지원됩니다. 새로 사용 하 **sp_addumpdevice** 이 매개 변수를 생략 해야 합니다.  
  
 [ **@devstatus =** ] **'***device_status***'**  
 더 이상 사용되지 않습니다. 지정된 경우 이 매개 변수는 무시됩니다. 이전 버전과의 호환성을 위해서만 지원됩니다. 새로 사용 하 **sp_addumpdevice** 이 매개 변수를 생략 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_addumpdevice** 백업 장치를 추가 하는 **sys.backup_devices** 카탈로그 뷰에 있습니다. 그런 다음 BACKUP 및 RESTORE 문에서 해당 장치를 논리적으로 참조할 수 있습니다. **sp_addumpdevice** 물리적 장치에 대 한 액세스를 수행 하지 않습니다. BACKUP 또는 RESTORE 문을 수행하는 경우에만 지정한 장치에 액세스합니다. 논리적 백업 장치를 만들면 "TAPE =" 또는 "DISK =" 절 대신 장치 이름을 사용하여 장치 경로를 지정할 수 있으므로 BACKUP 및 RESTORE 문이 간단해집니다.  
  
 소유권 및 사용 권한 문제가 디스크 또는 파일 백업 장치 사용을 방해하는 경우가 있습니다. 따라서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작된 Windows 계정에 대해 적절한 파일 사용 권한을 부여하십시오.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 Windows에서 지원되는 테이프 장치에 테이프 백업을 지원합니다. Windows에서 지원되는 테이프 장치에 관한 자세한 내용은 Windows의 하드웨어 호환성 목록을 참조하십시오. 컴퓨터에서 사용 가능한 테이프 장치를 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하십시오.  
  
 드라이브 제조업체가 권장하는 특정 테이프 드라이브에 대해서는 권장되는 테이프만 사용하십시오. DAT(디지털 오디오 테이프) 드라이브를 사용하는 경우 컴퓨터 등급 DAT 테이프(DDS: 디지털 데이터 저장소)를 사용하십시오.  
  
 **sp_addumpdevice** 트랜잭션 내에서 실행 될 수 없습니다.  
  
 사용 하 여 장치를 삭제 하려면 [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) 또는[SQL Server Management Studio](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 디스크에 대한 쓰기 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-disk-dump-device"></a>1. 디스크 덤프 장치 추가  
 다음 예에서는 `mydiskdump`이라는 물리적 이름으로 `c:\dump\dump1.bak`라는 디스크 백업 장치를 추가합니다.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak';  
```  
  
### <a name="b-adding-a-network-disk-backup-device"></a>2. 네트워크 디스크 백업 장치 추가  
 다음 예에서는 `networkdevice`라는 원격 디스크 백업 장치를 추가합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작되는 이름은 반드시 해당 원격 파일(`\\<servername>\<sharename>\<path>\<filename>.bak`)에 대한 사용 권한이 있어야 합니다.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'networkdevice',  
    '\\<servername>\<sharename>\<path>\<filename>.bak';  
```  
  
### <a name="c-adding-a-tape-backup-device"></a>3. 테이프 백업 장치 추가  
 다음 예에서는 `tapedump1`이라는 물리적 이름으로 `\\.\tape0` 장치를 추가합니다.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0';  
```  
  
### <a name="d-backing-up-to-a-logical-backup-device"></a>4. 논리적 백업 장치에 백업  
 다음 예에서는 백업 디스크 파일에 대해 논리적 백업 장치인 `AdvWorksData`를 만듭니다. 그런 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 이 논리적 백업 장치에 백업합니다.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\AdvWorksData.bak';  
GO  
BACKUP DATABASE AdventureWorks2012   
 TO AdvWorksData  
   WITH FORMAT;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sp_dropdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [sys.backup_devices&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
