---
title: sp_adddistributor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 45088122cfb6824598aaf40486264d41216d3c39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771317"
---
# <a name="sp_adddistributor-transact-sql"></a>sp_adddistributor(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [Sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) 테이블에 항목을 만들고 (없는 경우) 서버 항목을 배포자로 표시 하 고 속성 정보를 저장 합니다. 이 저장 프로시저는 서버를 배포자로 등록하고 표시하기 위해 master 데이터베이스의 배포자에서 실행됩니다. 원격 배포자의 경우도 마찬가지로, 원격 배포자를 등록하기 위해 master 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>인수  
`[ @distributor = ] 'distributor'`배포 서버 이름입니다. *배포자* 는 **sysname**이며 기본값은 없습니다. 이 매개 변수는 원격 배포자를 설정할 때에만 사용합니다. Msdb .의 배포자 속성에 대 한 항목을 추가 **합니다. MSdistributor** 테이블.  
  
`[ @heartbeat_interval = ] heartbeat_interval`진행률 메시지를 기록 하지 않고 에이전트를 진행할 수 있는 최대 시간 (분)입니다. *heartbeat_interval* 은 **int**이며 기본값은 10 분입니다. 실행 중인 복제 에이전트의 상태를 확인하기 위해 이 간격으로 실행되는 SQL Server 에이전트 작업이 생성됩니다.  
  
`[ @password = ] 'password']`**Distributor_admin** 로그인의 암호입니다. *password* 는 **sysname**이며 기본값은 NULL입니다. NULL 또는 빈 문자열인 경우 암호는 임의의 값으로 다시 설정됩니다. 암호는 첫 번째 원격 배포자가 추가될 때 구성되어야 합니다. 로컬 연결을 포함 하 여 *배포자* RPC 연결에 사용 되는 연결 된 서버 항목에 대 한 로그인 및 *암호* **distributor_admin** 저장 됩니다. *배포자* 가 로컬 이면 **distributor_admin** 의 암호가 새 값으로 설정 됩니다. 원격 배포자가 있는 게시자의 경우 게시자와 배포자에서 모두 **sp_adddistributor** 을 실행할 때 동일한 *password* 값을 지정 해야 합니다. [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) 를 사용 하 여 배포자 암호를 변경할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_adddistributor** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_adddistributor**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Transact-sql&#41;sp_changedistributor_property &#40;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistributor &#40;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistributor &#40;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
