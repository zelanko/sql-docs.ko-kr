---
title: sys.sysdatabases (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 57ddd4182fcfd3a2d85307df7a898c5d0a66a7e0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  인스턴스의 각 데이터베이스에 대해 하나의 행을 포함 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 처음 설치 **sysdatabases** 에 대 한 항목이 포함 되어는 **마스터**, **모델**, **msdb**, 및 **tempdb** 데이터베이스.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 이름|  
|**dbid**|**smallint**|데이터베이스 ID|  
|**sid**|**varbinary(85)**|데이터베이스를 만든 이의 시스템 ID입니다.|  
|**mode**|**smallint**|데이터베이스를 만드는 동안 잠그기 위해 내부적으로 사용됩니다.|  
|**상태**|**int**|그 중 일부를 사용 하 여 설정할 수 있습니다 상태 비트 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 언급 했 듯이:<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 = **에 선택 / bulkcopy** (ALTER DATABASE SET RECOVERY를 사용 하 여)<br /><br /> 8 = **trunc. 로그온에서 chkpt** (ALTER DATABASE SET RECOVERY를 사용 하 여)<br /><br /> 16 = **조각난 페이지 검색** (ALTER DATABASE)<br /><br /> 32 = **로드**<br /><br /> 64 = **pre recovery**<br /><br /> 128 = **recovering**<br /><br /> 256 = **복구 되지 않습니다**<br /><br /> 512 = **offline** (ALTER DATABASE)<br /><br /> 1024 = **읽기 전용** (ALTER DATABASE)<br /><br /> 2048 = **dbo 전용** (ALTER DATABASE SET RESTRICTED_USER를 사용 하 여)<br /><br /> 4096 = **단일 사용자** (ALTER DATABASE)<br /><br /> 32768 = **응급 모드**<br /><br /> 65536 = **체크섬** (ALTER DATABASE)<br /><br /> 4194304 = **autoshrink** (ALTER DATABASE)<br /><br /> 1073741824 = **종결**<br /><br /> 동시에 여러 비트를 설정할 수 있습니다.|  
|**status2**|**int**|16384 = **ANSI null 기본값** (ALTER DATABASE)<br /><br /> 65536 = **null 연결 시 null 생성** (ALTER DATABASE)<br /><br /> 131072 = **재귀 트리거** (ALTER DATABASE)<br /><br /> 1048576 = **기본적으로 로컬 커서** (ALTER DATABASE)<br /><br /> 8388608 = **따옴표 붙은 식별자** (ALTER DATABASE)<br /><br /> 33554432 = **커밋 시 커서 닫기** (ALTER DATABASE)<br /><br /> 67108864 = **ANSI nulls** (ALTER DATABASE)<br /><br /> 268435456 = **ANSI warnings** (ALTER DATABASE)<br /><br /> 536870912 = **텍스트를 사용할 수 전체** (사용 하 여 설정 **sp_fulltext_database**)|  
|**crdate**|**datetime**|만든 날짜입니다.|  
|**reserved**|**datetime**|나중에 사용하도록 예약되어 있습니다.|  
|**category**|**int**|복제에 사용되는 정보의 비트맵을 포함합니다.<br /><br /> 1 = 스냅숏 또는 트랜잭션 복제용으로 게시됩니다.<br /><br /> 2 = 스냅숏 또는 트랜잭션 게시를 구독합니다.<br /><br /> 4 = 병합 복제용으로 게시됩니다.<br /><br /> 8 = 병합 게시를 구독합니다.<br /><br /> 16 = 배포 데이터베이스입니다.|  
|**cmptlevel**|**tinyint**|데이터베이스의 호환성 수준입니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.|  
|**filename**|**nvarchar(260)**|데이터베이스 주 파일의 운영 체제 경로 및 이름입니다.<br /><br /> **filename** 을 볼 수 **dbcreator**, **sysadmin**, CREATE ANY DATABASE 권한 또는 권한 중 하나를 부여 된 사용자와 데이터베이스 소유자: ALTER ANY 데이터베이스, 모든 데이터베이스 만들기, 모든 정의 보기. 파일 이름과 경로 반환 하려면 쿼리는 [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md) 호환성 보기 또는 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 보기.|  
|**version**|**smallint**|데이터베이스가 만들어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드의 내부 버전 번호입니다. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [시스템 뷰 &#40; 시스템 테이블 매핑 Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
