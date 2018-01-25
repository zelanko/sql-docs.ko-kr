---
title: RESTORE REWINDONLY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_REWINDONLY_TSQL
- RESTORE REWINDONLY
dev_langs: TSQL
helpviewer_keywords:
- closing backup devices
- backup devices [SQL Server], rewinding
- media [SQL Server]
- open back devices
- rewinding backup devices
- RESTORE REWINDONLY statement
ms.assetid: 7f825b40-2264-4608-9809-590d0f09d882
caps.latest.revision: "50"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf67d54e58f08296878c0781158e7b878b0b2a49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---rewindonly-transact-sql"></a>RESTORE 문-REWINDONLY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  NOREWIND 옵션을 사용하여 실행된 BACKUP 또는 RESTORE 문에 의해 열려 있는 지정한 테이프 장치를 되감아 닫습니다. 이 명령은 테이프 장치에서만 지원됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE REWINDONLY   
FROM <backup_device> [ ,...n ]  
[ WITH {UNLOAD | NOUNLOAD}]  
}   
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | TAPE = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}   
```  
  
## <a name="arguments"></a>인수  
 **\<backup_device> ::=** 
  
 복원 작업에 사용할 논리적 또는 물리적 백업 장치를 지정합니다.  
  
 { *logical_backup_device_name* | **@ * * * logical_backup_device_name_var* } 식별자 백업 장치에 대 한 규칙을 따라야 하는 논리적 이름 만든 **sp_addumpdevice** 에서 데이터베이스를 복원 합니다. 변수로 제공한 경우 (**@***logical_backup_device_name_var*), 백업 장치 이름은 문자열 상수를 지정 (**@ * * * logical_backup_device_name_var*  =   *logical_backup_device_name*) 또는 문자 문자열 데이터 형식의 변수를 제외 하 고는 **ntext** 또는 **텍스트** 데이터 형식입니다.  
  
 {디스크 | 테이프}  **=**  { **'***physical_backup_device_name***'** | **@ * * * physical_backup_device_name_var*  } 백업이 지정된 된 디스크 또는 테이프 장치에서 복원할 수 있습니다. 디스크 및 테이프의 장치 유형은 장치의 실제 이름 (예를 들어 전체 경로 및 파일 이름)으로 지정 해야: 디스크 = ' C:\Program Files\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' 또는 TAPE = '\\\\. \TAPE0'. 변수로 지정 된 경우 (**@***physical_backup_device_name_var*), 장치 이름은 문자열 상수를 지정 (**@ * * * physical_backup_device_name_var* = '* physcial_backup_device_name *') 또는 문자 문자열 데이터 형식의 변수를 제외 하 고는 **ntext** 또는 **텍스트** 데이터 형식입니다.  
  
 네트워크 서버에 UNC 이름(컴퓨터 이름 포함)을 사용하는 경우 디스크의 장치 유형을 지정합니다. UNC 이름 사용 하는 방법에 대 한 자세한 내용은 참조 [백업 장치 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 Microsoft SQL Server 실행 중인 계정에는 복원 작업을 수행 하려면 원격 컴퓨터나 네트워크 서버에 대 한 읽기 액세스 있어야 합니다.  
  
 *n*  
 여러 백업 장치와 논리적 백업 장치를 지정할 수 있음을 나타내는 자리 표시자입니다. 백업 장치 또는 논리적 백업 장치의 최대는 **64**합니다.  
  
 오프라인 복원인지 온라인 복원인지에 따라, 복원 시퀀스에서 백업이 속한 미디어 세트를 만들 때 사용된 개수만큼 백업 장치가 필요한지 결정됩니다. 오프라인 복원의 경우 백업을 만들 때 보다 적은 장치를 사용하여 백업을 복원할 수 있습니다. 온라인 복원의 경우 백업을 만들 때 사용된 백업 장치가 모두 필요합니다. 필요한 장치를 모두 사용하지 않으면 복원이 실패합니다.  
  
 자세한 내용은 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)인스턴스를 실행하는 컴퓨터에 테이프 드라이브가 연결되어 있는 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  미러된 미디어 세트의 백업을 복원하려는 경우 각 미디어 패밀리에 하나의 미러만 지정할 수 있습니다. 그러나 오류가 발생할 때 다른 미러가 있으면 일부 복원 문제를 빨리 해결할 수 있습니다. 손상된 미디어 볼륨은 다른 미러에서 상응하는 볼륨으로 대체할 수 있습니다. 오프라인 복원의 경우 미디어 패밀리보다 적은 장치에서 복원할 수 있으나 각 패밀리는 한 번만 처리됩니다.  
  
 **WITH 옵션**  
  
 UNLOAD  
 RESTORE가 끝나면 테이프를 자동으로 되감고 언로드되도록 지정합니다. 새로운 사용자 세션을 시작할 경우 기본적으로 UNLOAD로 설정되며 NOUNLOAD를 지정할 때까지 UNLOAD로 설정되어 있습니다. 이 옵션은 테이프 장치에서만 사용합니다. RESTORE에 테이프 이외의 장치를 사용할 경우 이 옵션은 무시됩니다.  
  
 NOUNLOAD  
 RESTORE 후 테이프가 테이프 드라이브에서 자동으로 언로드되지 않게 지정합니다. UNLOAD를 지정할 때까지 NOUNLOAD로 설정되어 있습니다.  
  
 RESTORE 후 테이프가 테이프 드라이브에서 자동으로 언로드되지 않게 지정합니다. UNLOAD를 지정할 때까지 NOUNLOAD로 설정되어 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 RESTORE REWINDONLY는 RESTORE LABELONLY FROM TAPE 하는 대신 = \<이름 > WITH REWIND입니다. 열려 있는 테이프 드라이브의 목록을 가져올 수는 [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 동적 관리 뷰.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 모든 사용자가 RESTORE REWINDONLY를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

