---
description: sp_addscriptexec(Transact-SQL)
title: sp_addscriptexec (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81d3b8ac9e8eda12ed27099fed5623d0fd3da489
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536766"
---
# <a name="sp_addscriptexec-transact-sql"></a>sp_addscriptexec(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  게시의 모든 구독자에 SQL 스크립트(.sql 파일)를 게시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @scriptfile = ] 'scriptfile'` SQL 스크립트 파일의 전체 경로입니다. *scriptfile* 는 **nvarchar (4000)** 이며 기본값은 없습니다.  
  
`[ @skiperror = ] 'skiperror'` 스크립트를 처리 하는 동안 오류가 발생 하는 경우 배포 에이전트 또는 병합 에이전트를 중지할지 여부를 나타냅니다. *SkipError* 는 **bit**이며 기본값은 0입니다.  
  
 **0** = 에이전트가 중지 됩니다.  
  
 **1** = 에이전트가 스크립트를 계속 하 고 오류를 무시 합니다.  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에서 게시할 때는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addscriptexec** 은 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 **sp_addscriptexec** 는 스냅숏 복제에 사용 되지 않습니다.  
  
 **Sp_addscriptexec**를 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 스냅숏 위치에 대 한 읽기 및 쓰기 권한과 스크립트가 저장 된 위치에 대 한 읽기 권한이 있어야 합니다.  
  
 [Sqlcmd 유틸리티](../../tools/sqlcmd-utility.md) 는 구독자에서 스크립트를 실행 하는 데 사용 되며, 구독 데이터베이스에 연결할 때 배포 에이전트 또는 병합 에이전트에서 사용 되는 보안 컨텍스트에서 스크립트가 실행 됩니다. 에이전트가 이전 버전의에서 실행 되는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [sqlcmd](../../tools/sqlcmd-utility.md)대신 [osql 유틸리티가](../../tools/osql-utility.md) 사용 됩니다.  
  
 **sp_addscriptexec** 는 구독자에 스크립트를 적용 하는 데 유용 하며 [sqlcmd](../../tools/sqlcmd-utility.md) 를 사용 하 여 스크립트의 내용을 구독자에 적용 합니다. 하지만 구독자 구성은 다양할 수 있으므로 게시자에 게시하기 전에 테스트한 스크립트도 구독자에서 오류를 일으킬 수 있습니다. *skiperror* 는 배포 에이전트 또는 병합 에이전트 오류를 무시 하 고 계속 진행할 수 있는 기능을 제공 합니다. **Sp_addscriptexec**를 실행 하기 전에 [sqlcmd](../../tools/sqlcmd-utility.md) 를 사용 하 여 스크립트를 테스트 합니다.  
  
> [!NOTE]  
>  오류 건너뛰기는 에이전트 기록에 참조로 계속 기록됩니다.  
  
 스냅숏 배달에 FTP를 사용 하는 게시에 대 한 스크립트 파일을 게시 하기 위해 **sp_addscriptexec** 를 사용 하는 것은 구독자 에서만 지원 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addscriptexec**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 Transact-sql 프로그래밍 &#40;동기화 중 스크립트 실행&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
