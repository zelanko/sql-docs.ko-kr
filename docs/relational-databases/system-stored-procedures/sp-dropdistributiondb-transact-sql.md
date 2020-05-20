---
title: sp_dropdistributiondb (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7171c1e80260f28f85e2b7490f7ac21bea217173
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830177"
---
# <a name="sp_dropdistributiondb-transact-sql"></a>sp_dropdistributiondb(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  배포 데이터베이스를 삭제합니다. 다른 데이터베이스에 해당 물리적 파일이 사용되지 않는 경우에 한해 데이터베이스에 사용되는 물리적 파일을 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>인수  
`[ @database = ] 'database'`삭제할 데이터베이스입니다. *데이터베이스* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropdistributiondb** 은 모든 유형의 복제에 사용 됩니다.  
  
 이 저장 프로시저는 **sp_dropdistributor**를 실행 하 여 배포자를 삭제 하기 전에 실행 해야 합니다.  
  
 또한 **sp_dropdistributiondb** 는 배포 데이터베이스 (있는 경우)에 대 한 큐 판독기 에이전트 작업을 제거 합니다.  
  
 배포를 사용하지 않으려면 배포 데이터베이스가 온라인 상태여야 합니다. 배포 데이터베이스에 대해 데이터베이스 스냅샷이 있으면 배포를 사용하지 않도록 설정하기 전에 이 스냅샷을 먼저 삭제해야 합니다. 데이터베이스 스냅샷은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅샷과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅샷&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dropdistributiondb**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Transact-sql&#41;sp_adddistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_changedistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
