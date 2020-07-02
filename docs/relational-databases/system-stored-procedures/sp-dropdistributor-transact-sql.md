---
title: sp_dropdistributor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fdd3c733d93fa803906523d7150b4377e6f28666
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786935"
---
# <a name="sp_dropdistributor-transact-sql"></a>sp_dropdistributor(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포자를 제거합니다. 이 저장 프로시저는 배포 데이터베이스를 제외한 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
`[ @no_checks = ] no_checks`배포자를 삭제 하기 전에 종속 개체를 확인할 지 여부를 나타냅니다. *no_checks* 은 **bit**이며 기본값은 0입니다.  
  
 **0**인 경우, **sp_dropdistributor** 배포자와 함께 모든 게시 및 배포 개체가 삭제 되었는지 확인 합니다.  
  
 **1**인 경우 **sp_dropdistributor** 배포자를 제거 하기 전에 모든 게시 및 배포 개체를 삭제 합니다.  
  
`[ @ignore_distributor = ] ignore_distributor`이 저장 프로시저가 배포자에 연결 되지 않고 실행 되는지 여부를 나타냅니다. *ignore_distributor* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0**인 경우 **sp_dropdistributor** 배포자에 연결 하 고 모든 복제 개체를 제거 합니다. **Sp_dropdistributor** 배포자에 연결할 수 없는 경우 저장 프로시저가 실패 합니다.  
  
 **1**인 경우 배포자에 대 한 연결이 설정 되지 않으며 복제 개체는 제거 되지 않습니다. 배포자가 제거되었거나 영구적으로 오프라인 상태인 경우에 사용합니다. 배포자에서 게시자에 대한 개체는 배포자가 나중에 다시 설치될 때까지 제거되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropdistributor** 은 모든 유형의 복제에 사용 됩니다.  
  
 서버에 다른 게시자 또는 배포 개체가 있는 경우 ** \@ no_checks** **1**로 설정 되어 있지 않으면 **sp_dropdistributor** 실패 합니다.  
  
 이 저장 프로시저는 **sp_dropdistributiondb**를 실행 하 여 배포 데이터베이스를 삭제 한 후에 실행 해야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dropdistributor**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Transact-sql&#41;sp_adddistributor &#40;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Transact-sql&#41;sp_changedistributor_property &#40;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistributor &#40;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
