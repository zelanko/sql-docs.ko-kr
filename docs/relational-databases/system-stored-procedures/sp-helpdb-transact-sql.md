---
title: sp_helpdb (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09dc7e451e5122600b0ea32222f6fa913c2716f8
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027707"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스 또는 모든 데이터베이스에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@dbname=** ] **'***name***'**  
 정보를 보고할 대상 데이터베이스의 이름입니다. *이름을* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 *이름* 지정 하지 않으면 **sp_helpdb** 에 있는 모든 데이터베이스에서 보고서를 **sys.databases** 카탈로그 뷰.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 이름입니다.|  
|**db_size**|**nvarchar(13)**|데이터베이스의 총 크기입니다.|  
|**소유자**|**sysname**|데이터베이스 소유자와 같은 **sa**합니다.|  
|**dbid**|**smallint**|데이터베이스 ID입니다.|  
|**created**|**nvarchar(11)**|데이터베이스가 만들어진 날짜입니다.|  
|**상태**|**nvarchar(600)**|현재 데이터베이스에 설정된 데이터베이스 옵션의 값을 쉼표로 분리하여 나열한 것입니다.<br /><br /> 부울 값 옵션은 활성화된 경우에만 나열됩니다. 부울이 아닌 옵션의 형태로 해당 값을 사용 하 여 나와 *option_name*=*값*합니다.<br /><br /> 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.|  
|**compatibility_level**|**tinyint**|데이터베이스 호환성 수준: 60, 65, 70, 80 또는 90입니다.|  
  
 하는 경우 *이름을* 이 지정 되어 있는 지정된 된 데이터베이스에 대 한 파일 할당을 보여 주는 추가 결과 집합은입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|논리적 파일 이름입니다.|  
|**fileid**|**smallint**|파일의 ID입니다.|  
|**filename**|**nchar(260)**|운영 체제 파일 이름(물리적 파일 이름)입니다.|  
|**filegroup**|**nvarchar(128)**|파일이 속한 파일 그룹입니다.<br /><br /> NULL = 로그 파일이며 파일 그룹에 속하지 않습니다.|  
|**size**|**nvarchar(18)**|파일 크기(MB)입니다.|  
|**maxsize**|**nvarchar(18)**|파일이 증가할 수 있는 최대 크기입니다. 이 필드 값이 UNLIMITED이면 디스크가 꽉 찰 때까지 파일이 증가할 수 있음을 의미합니다.|  
|**growth**|**nvarchar(18)**|파일의 증가분입니다. 공간이 새로 필요할 때마다 파일에 추가되는 공간의 양입니다.|  
|**사용 현황**|**varchar(9)**|파일의 용도입니다. 데이터 파일에 대 한 값이 **'데이터만'** 하 고 값은 로그 파일에 대 한 **'로그'** 합니다.|  
  
## <a name="remarks"></a>Remarks  
 합니다 **상태** 결과의 열을 데이터베이스에는 옵션이 ON으로 설정 되어 있는 보고서를 설정 합니다. 가 모든 데이터베이스 옵션을 보고 하지 않는 합니다 **상태** 열입니다. 현재 데이터베이스 옵션 설정의 전체 목록을 보려면를 사용 합니다 **sys.databases** 카탈로그 뷰.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격, 단일 데이터베이스를 지정 하는 경우는 **공용** 데이터베이스 역할에에서 필요 합니다. 데이터베이스가 지정 되지 않은, 경우 자격이 **공용** 역할에는 **마스터** 데이터베이스가 필요 합니다.  
  
 데이터베이스에 액세스할 수 없으면 **sp_helpdb** 수 있으므로 데이터베이스에 대 한 오류 메시지 15622와 많은 정보를 표시 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-information-about-a-single-database"></a>1. 단일 데이터베이스에 대한 정보 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 정보를 표시합니다.  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>2. 모든 데이터베이스에 대한 정보 반환  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 서버에 있는 모든 데이터베이스에 대한 정보를 표시합니다.  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
