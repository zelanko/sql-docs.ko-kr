---
title: sp_wait_for_database_copy_sync
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-dt-2019
ms.openlocfilehash: 931babcaa6e229d6114930bba5f06803aa25f59e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829686"
---
# <a name="active-geo-replication---sp_wait_for_database_copy_sync"></a>활성 지역 복제-sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  이 프로시저는 기본 및 보조 간 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 관계로 한정됩니다. **Sp_wait_for_database_copy_sync** 를 호출 하면 모든 커밋된 트랜잭션이 활성 보조 데이터베이스에서 복제 되 고 승인 될 때까지 응용 프로그램이 대기 합니다. 주 데이터베이스 에서만 **sp_wait_for_database_copy_sync** 를 실행 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>구문  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>인수  
 [ @target_server =] ' server_name '  
 활성 보조 데이터베이스를 호스트하는 SQL Database 서버의 이름입니다. server_name은 sysname이며 기본값은 없습니다.  
  
 [ @target_database = ] 'database_name'  
 활성 보조 데이터베이스의 이름입니다. database_name은 sysname이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공하면 0을 반환하고 실패하면 오류 번호를 반환합니다.  
  
 가장 가능성이 높은 오류 조건은 다음과 같습니다.  
  
-   서버 이름 또는 데이터베이스 이름이 없는 경우  
  
-   지정된 서버 이름 또는 데이터베이스에 대한 링크를 찾을 수 없는 경우  
  
-   상호 링크 연결이 손실된 경우. 연결 제한 시간 후에 **sp_wait_for_database_copy_sync** 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 주 데이터베이스의 모든 사용자가 이 시스템 저장 프로시저를 호출할 수 있습니다. 로그인은 기본 및 활성 보조 데이터베이스 둘 다에 있는 사용자여야 합니다.  
  
## <a name="remarks"></a>설명  
 **Sp_wait_for_database_copy_sync** 호출 전에 커밋된 모든 트랜잭션이 활성 보조 데이터베이스에 전송 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **sp_wait_for_database_copy_sync** 를 호출 하 여 모든 트랜잭션이 주 데이터베이스인 d b 0에서 대상 서버 ubfyu5ssyt의 활성 보조 데이터베이스로 전송 되도록 합니다.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [dm_continuous_copy_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [지역에서 복제 Dmv (동적 관리 뷰) 및 함수 &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status](../system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)
  
  
