---
title: sp_showrowreplicainfo (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 80e50ddc736ee63c893fdd3b6a785503c2f17c7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제에서 아티클로 사용될 테이블의 행에 대한 정보를 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@ownername**=] **'***ownername***'**  
 테이블 소유자의 이름입니다. *ownername* 은 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 데이터베이스에 이름은 같지만 소유자는 다른 여러 개의 테이블이 있는 경우 테이블을 구별하는 데 유용합니다.  
  
 [  **@tablename =**] **'***tablename***'**  
 정보가 반환되는 대상 행을 포함하는 테이블의 이름입니다. *tablename* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@rowguid =**] *rowguid*  
 행의 고유 식별자입니다. *rowguid* 은 **uniqueidentifier**, 기본값은 없습니다.  
  
 [ **@show**=] **'***표시***'**  
 결과 집합으로 반환될 정보의 양을 결정합니다. *표시* 은 **nvarchar (20)** 둘 다의 기본값입니다. 경우 **행**, 행 버전 정보만 반환 됩니다. 경우 **열**, 열 버전 정보만 반환 됩니다. 경우 **둘 다**, 둘 다 행 및 열 정보가 반환 됩니다.  
  
## <a name="result-sets-for-row-information"></a>행 정보에 대한 결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|행 버전 항목을 만든 데이터베이스를 호스팅하는 서버의 이름입니다.|  
|**db_name**|**sysname**|이 항목을 만든 데이터베이스의 이름입니다.|  
|**db_nickname**|**binary(6)**|이 항목을 만든 데이터베이스의 애칭입니다.|  
|**version**|**int**|항목의 버전입니다.|  
|**current_state**|**nvarchar(9)**|행의 현재 상태에 대한 정보를 반환합니다.<br /><br /> **y** -행 데이터가 행의 현재 상태를 나타냅니다.<br /><br /> **n** -행 데이터가 행의 현재 상태를 나타내지 않습니다.<br /><br /> **\<n/a >** -적용할 수 없음.<br /><br /> **\<알 수 없는 >** -현재 상태를 확인할 수 없습니다.|  
|**rowversion_table**|**nchar(17)**|행 버전에 저장 된 있는지 여부를 나타내는 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 테이블 또는 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 테이블입니다.|  
|**주석**|**nvarchar(255)**|현재 행 버전 항목에 대한 추가 정보입니다. 일반적으로 이 필드는 비어 있습니다.|  
  
## <a name="result-sets-for-column-information"></a>열 정보에 대한 결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|열 버전 항목을 만든 데이터베이스를 호스팅하는 서버의 이름입니다.|  
|**db_name**|**sysname**|이 항목을 만든 데이터베이스의 이름입니다.|  
|**db_nickname**|**binary(6)**|이 항목을 만든 데이터베이스의 애칭입니다.|  
|**version**|**int**|항목의 버전입니다.|  
|**colname**|**sysname**|열 버전 항목이 표시되는 아티클 열의 이름입니다.|  
|**주석**|**nvarchar(255)**|이 열 버전 항목에 대한 추가 정보입니다. 일반적으로 이 필드는 비어 있습니다.|  
  
## <a name="result-set-for-both"></a>두 가지 모두에 대한 결과 집합  
 경우 값 **둘 다** 을 위해 선택한 *표시*, 행과 열 결과 집합이 반환 됩니다.  
  
## <a name="remarks"></a>주의  
 **sp_showrowreplicainfo** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo** 의 구성원만 실행할 수는 **db_owner** 게시 데이터베이스의 게시 액세스 목록 (PAL)의 멤버 또는 게시 데이터베이스의 고정된 데이터베이스 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
