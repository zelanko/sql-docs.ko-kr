---
title: sp_adddistributor (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 49b2250ac8c6a6ec634c1e141c28cc5056a80a24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 항목을 만듭니다는 [sys.sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) 테이블 (없는 경우 하나) 배포자로 서버 항목을 표시 하 고 속성 정보를 저장 합니다. 이 저장 프로시저는 서버를 배포자로 등록하고 표시하기 위해 master 데이터베이스의 배포자에서 실행됩니다. 원격 배포자의 경우도 마찬가지로, 원격 배포자를 등록하기 위해 master 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@distributor=**] **'***배포자***'**  
 배포자 서버 이름입니다. *배포자* 은 **sysname**, 기본값은 없습니다. 이 매개 변수는 원격 배포자를 설정할 때에만 사용합니다. 배포자 속성에 대 한 항목 추가 **msdb... MSdistributor** 테이블입니다.  
  
 [  **@heartbeat_interval=**] *heartbeat_interval*  
 진행률 메시지를 기록하지 않고 에이전트를 실행할 수 있는 최대 시간(분)입니다. *heartbeat_interval* 은 **int**, 기본값은 10 분입니다. 실행 중인 복제 에이전트의 상태를 확인하기 위해 이 간격으로 실행되는 SQL Server 에이전트 작업이 생성됩니다.  
  
 [  **@password=**] **'***암호***'**]  
 암호는 **distributor_admin** 로그인 합니다. *암호* 은 **sysname**, 기본값은 NULL입니다. NULL 또는 빈 문자열인 경우 암호는 임의의 값으로 다시 설정됩니다. 암호는 첫 번째 원격 배포자가 추가될 때 구성되어야 합니다. **distributor_admin** 로그인 및 *암호* 에 사용 되는 연결 된 서버 항목에 대해 저장 되는 *배포자* RPC 연결에 대 한 로컬 연결을 포함 합니다. 경우 *배포자* 가 로컬인 경우에 대 한 암호 **distributor_admin** 새 값으로 설정 됩니다. 원격 배포자로 게시자의 경우 변수에 같은 값 *암호* 를 실행할 때 지정 해야 **sp_adddistributor** 게시자와 배포자 모두에서 합니다. [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) 는 배포자 암호를 변경 하는 데 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [  **@from_scripting=** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_adddistributor** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_adddistributor**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
