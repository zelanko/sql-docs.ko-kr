---
description: sp_helpdistributiondb(Transact-SQL)
title: sp_helpdistributiondb (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c79c1ed5bbbbf53be84432e4d542affece0b16a3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543323"
---
# <a name="sp_helpdistributiondb-transact-sql"></a>sp_helpdistributiondb(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  지정한 배포 데이터베이스의 속성을 반환합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @database = ] 'database_name'` 속성이 반환 되는 데이터베이스 이름입니다. *database_name* 는 **Sysname**이며, **%** 배포자와 연결 되어 있고 사용자에 게 권한이 있는 모든 데이터베이스의 기본값은입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**min_distretention**|**int**|트랜잭션을 삭제하기 전 최소 보존 기간(시간)을 표시합니다.|  
|**max_distretention**|**int**|트랜잭션을 삭제하기 전 최대 보존 기간(시간)을 표시합니다.|  
|**history retention**|**int**|기록을 보존할 기간(시간)입니다.|  
|**history_cleanup_agent**|**sysname**|기록 정리 에이전트의 이름입니다.|  
|**distribution_cleanup_agent**|**sysname**|배포 정리 에이전트의 이름입니다.|  
|**status**|**int**|내부적으로만 사용됩니다.|  
|**data_folder**|**nvarchar(255)**|데이터베이스 파일을 저장하는 데 사용되는 디렉터리 이름입니다.|  
|**data_file**|**nvarchar(255)**|데이터베이스 파일의 이름입니다.|  
|**data_file_size**|**int**|초기 데이터 파일의 크기(MB)입니다.|  
|**log_folder**|**nvarchar(255)**|데이터베이스 로그 파일의 디렉터리 이름입니다.|  
|**log_file**|**nvarchar(255)**|로그 파일의 이름입니다.|  
|**log_file_size**|**int**|초기 로그 파일의 크기(MB)입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpdistributiondb** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 또는 배포 데이터베이스에 있는 **replmonitor** 역할의 멤버 및 배포 데이터베이스를 사용 하는 게시의 게시 액세스 목록에 있는 사용자는 **sp_helpdistributiondb** 를 실행 하 여 파일 관련 정보를 반환할 수 있습니다. **Public** 역할의 멤버는 **sp_helpdistributiondb** 를 실행 하 여 액세스 권한이 있는 배포 데이터베이스에 대 한 파일 관련 없는 정보를 반환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Transact-sql&#41;sp_adddistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_changedistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
