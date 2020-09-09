---
description: sp_setsubscriptionxactseqno(Transact-SQL)
title: sp_setsubscriptionxactseqno (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c7908e6cc064a5ad5c973236be759bdea313c5f6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547905"
---
# <a name="sp_setsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  문제를 해결 하는 동안 사용 되어 배포 에이전트 LSN (로그 시퀀스 번호)을 사용 하 여 마지막으로 배달 된 트랜잭션을 지정 하 여 다음 트랜잭션에 배달 될 수 있도록 합니다. 다시 시작할 때 배포 에이전트는 배포 데이터베이스 캐시 (msrepl_commands)에서이 워터 마크 (LSN) 보다 큰 트랜잭션을 반환 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. SQL Server 이외 게시자에 대해서는 지원되지 않습니다.  
  
> [!CAUTION]  
>  이 저장 프로시저를 잘못 사용하거나 잘못된 LSN 값을 지정하면 배포 에이전트에서 구독자에 이미 적용된 변경 사항이 취소되거나 나머지 모든 변경 사항을 건너뛸 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다. SQL Server 이외 *Publisher_db* 게시자의 경우는 배포 데이터베이스의 이름입니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. 배포 에이전트 둘 이상의 게시에서 공유 되는 경우 *게시*에 대해 모두 값을 지정 해야 합니다.  
  
`[ @xact_seqno = ] xact_seqno` 배포자에서 구독자에 적용 될 다음 트랜잭션의 LSN입니다. *xact_seqno* 는 **varbinary (16)** 이며 기본값은 없습니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|구독자에 적용될 다음 트랜잭션의 원래 LSN입니다.|  
|**UPDATED XACT_SEQNO**|**varbinary(16)**|구독자에 적용될 다음 트랜잭션의 업데이트된 LSN입니다.|  
|**SUBSCRIPTION STREAM COUNT**|**int**|마지막 동기화 중에 사용된 구독 스트림의 수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_setsubscriptionxactseqno** 은 트랜잭션 복제에 사용 됩니다.  
  
 피어 투 피어 트랜잭션 복제 토폴로지에서는 **sp_setsubscriptionxactseqno** 사용할 수 없습니다.  
  
 **sp_setsubscriptionxactseqno** 를 사용 하 여 구독자에 적용 될 때 오류가 발생 하는 특정 트랜잭션을 건너뛸 수 있습니다. 오류가 발생 하 고 배포 에이전트 중지 된 후에는 배포자에서 [transact-sql&#41;&#40;sp_helpsubscriptionerrors ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) 를 호출 하 여 실패 한 트랜잭션의 xact_seqno 값을 검색 한 다음 **sp_setsubscriptionxactseqno**를 호출 하 여 *xact_seqno*에 대해이 값을 전달 합니다. 그러면 이 LSN 이후의 명령만 처리됩니다.  
  
 배포 데이터베이스에서 보류 중인 모든 명령을 구독자로 배달 하려면 *xact_seqno* 값을 **0** 으로 지정 합니다.  
  
 배포 에이전트에서 다중 구독 스트림을 사용 하는 경우 **sp_setsubscriptionxactseqno** 실패할 수 있습니다.  
  
 이 오류가 발생하면 단일 구독 스트림으로 배포 에이전트를 실행해야 합니다. 자세한 내용은 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_setsubscriptionxactseqno**을 실행할 수 있습니다.  
  
## <a name="see-more"></a>자세히 보기

[블로그: 트랜잭션을 건너뛰는 방법](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  
