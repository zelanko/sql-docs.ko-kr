---
title: sp_addscriptexec (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36188e2faa578c0c4ef2a89b32e00d474366d32d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212442"
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시의 모든 구독자에 SQL 스크립트(.sql 파일)를 게시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=** ] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@scriptfile=** ] **'***scriptfile***'**  
 SQL 스크립트 파일의 전체 경로입니다. *scriptfile* 됩니다 **nvarchar(4000)**, 기본값은 없습니다.  
  
 [  **@skiperror=** ] **'***skiperror***'**  
 스크립트가 처리되는 동안 오류가 발생하면 배포 에이전트 또는 병합 에이전트를 중지할지 여부를 나타냅니다. *SkipError* 됩니다 **비트**, 기본값은 0입니다.  
  
 **0** = 중지 됩니다.  
  
 **1** = 에이전트 스크립트를 계속 하 고 오류를 무시 합니다.  
  
 [  **@publisher=** ] **'***게시자***'**  
 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 게시 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addscriptexec** 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 **sp_addscriptexec** 스냅숏 복제에 사용 되지 않습니다.  
  
 사용 하도록 **sp_addscriptexec**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정이 읽기 있어야 하며 스크립트가 위치에 스냅숏 위치 및 읽기 권한에 대 한 쓰기 권한이 저장 됩니다.  
  
 합니다 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md) 구독자에서 스크립트를 실행 하는 스크립트는 구독 데이터베이스에 연결할 때 배포 에이전트 또는 병합 에이전트에서 사용 되는 보안 컨텍스트에서 실행 됩니다. 에이전트의 이전 버전에서 실행 되는 시점 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서 [osql 유틸리티](../../tools/osql-utility.md) 대신 사용 됩니다 [sqlcmd](../../tools/sqlcmd-utility.md)합니다.  
  
 **sp_addscriptexec** 구독자에 스크립트를 적용할 때 유용 하며 사용 [sqlcmd](../../tools/sqlcmd-utility.md) 스크립트의 내용을 구독자에 적용 합니다. 하지만 구독자 구성은 다양할 수 있으므로 게시자에 게시하기 전에 테스트한 스크립트도 구독자에서 오류를 일으킬 수 있습니다. *skiperror* 배포 에이전트 또는 병합 에이전트가 오류를 무시 하 고 계속 하는 기능을 제공 합니다. 사용 하 여 [sqlcmd](../../tools/sqlcmd-utility.md) 실행 하기 전에 스크립트를 테스트 하려면 **sp_addscriptexec**합니다.  
  
> [!NOTE]  
>  오류 건너뛰기는 에이전트 기록에 참조로 계속 기록됩니다.  
  
 사용 하 여 **sp_addscriptexec** 스냅숏 배달에 대해서만 지원 됩니다에 대 한 FTP를 사용 하 여 게시에 대 한 스크립트 파일을 게시할 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addscriptexec**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [동기화 중 스크립트 실행 &#40;복제 TRANSACT-SQL 프로그래밍&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
