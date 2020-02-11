---
title: sysdatabases (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b0dab1ca5f21ced6a54192a4b0173ead68fd6f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68089160"
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  인스턴스의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]각 데이터베이스에 대해 하나의 행을 포함 합니다. 가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 처음 설치 되 면 **sysdatabases** 에 **master**, **model**, **msdb**및 **tempdb** 데이터베이스에 대 한 항목이 포함 됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 이름|  
|**dbid**|**smallint**|데이터베이스 ID|  
|**s**|**varbinary (85)**|데이터베이스를 만든 이의 시스템 ID입니다.|  
|**모드가**|**smallint**|데이터베이스를 만드는 동안 잠그기 위해 내부적으로 사용됩니다.|  
|**업무**|**int**|상태 비트는 다음과 같이 [ALTER database](../../t-sql/statements/alter-database-transact-sql.md) 를 사용 하 여 설정할 수 있습니다.<br /><br /> 1 = **autoclose** (ALTER database)<br /><br /> 4 = **select into/대량 복사** (SET RECOVERY를 사용한 ALTER database)<br /><br /> 8 = **trunc on chkpt** (SET RECOVERY를 사용한 ALTER database)<br /><br /> 16 = **조각난 페이지 검색** (ALTER database)<br /><br /> 32 = **로드 중**<br /><br /> 64 = **사전 복구**<br /><br /> 128 = **복구** 중<br /><br /> 256 = **복구 되지 않음**<br /><br /> 512 = **오프 라인** (ALTER database)<br /><br /> 1024 = **읽기 전용** (ALTER database)<br /><br /> 2048 = **dbo use only** (SET RESTRICTED_USER를 사용한 ALTER database)<br /><br /> 4096 = **단일 사용자** (ALTER database)<br /><br /> 32768 = **응급 모드**<br /><br /> 65536 = **체크섬** (ALTER database)<br /><br /> 4194304 = 자동 **축소** (ALTER database)<br /><br /> 1073741824 = **완전히 종료**<br /><br /> 동시에 여러 비트를 설정할 수 있습니다.|  
|**status2**|**int**|16384 = **ANSI null 기본값** (ALTER database)<br /><br /> 65536 = **null을 생성 하면 null이 생성** 됩니다 (ALTER database).<br /><br /> 131072 = **재귀 트리거** (ALTER database)<br /><br /> 1048576 = **로컬 커서로 기본값** (ALTER database)<br /><br /> 8388608 = **따옴표 붙은 식별자** (ALTER database)<br /><br /> 33554432 = **커밋 시 커서 닫기** (ALTER database)<br /><br /> 67108864 = **ANSI null** (ALTER database)<br /><br /> 268435456 = **ANSI 경고** (ALTER database)<br /><br /> 536870912 = **전체 텍스트 사용** ( **sp_fulltext_database**를 사용 하 여 설정)|  
|**crdate**|**datetime**|만든 날짜입니다.|  
|**쓰이는**|**datetime**|향후 사용을 위해 예약되어 있습니다.|  
|**범주**|**int**|복제에 사용되는 정보의 비트맵을 포함합니다.<br /><br /> 1 = 스냅샷 또는 트랜잭션 복제용으로 게시됩니다.<br /><br /> 2 = 스냅샷 또는 트랜잭션 게시를 구독합니다.<br /><br /> 4 = 병합 복제용으로 게시됩니다.<br /><br /> 8 = 병합 게시를 구독합니다.<br /><br /> 16 = 배포 데이터베이스입니다.|  
|**cmptlevel**|**tinyint**|데이터베이스의 호환성 수준입니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.|  
|**이름도**|**nvarchar(260)**|데이터베이스 주 파일의 운영 체제 경로 및 이름입니다.<br /><br /> **filename** 은 **dbcreator**, **sysadmin**, 데이터베이스 소유자에 게 CREATE ANY DATABASE 권한 또는 피부 여자 (ALTER any DATABASE, CREATE any database, VIEW any DEFINITION) 중 하나가 포함 된 데이터베이스 소유자에 게 표시 됩니다. 경로 및 파일 이름을 반환 하려면 [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md) 호환성 뷰 또는 [sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 뷰를 쿼리 합니다.|  
|**버전**|**smallint**|데이터베이스가 만들어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드의 내부 버전 번호입니다. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
