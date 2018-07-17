---
title: CHECKPOINT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0cde74c2a82ae77b1bc417ba9642dd3632c2f435
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781274"
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 수동 검사점을 생성합니다.  
  
> [!NOTE]  
>  데이터베이스 검사점의 여러 유형과 일반적인 검사점 작업에 대한 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>인수  
 *checkpoint_duration*  
 수동 검사점을 완료하기 위해 요청된 시간(초)을 지정합니다. *checkpoint_duration*을 지정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 요청된 기간 내에 검사점을 수행하려고 시도합니다. *checkpoint_duration*은 **int** 형식의 식이어야 하며 0보다 커야 합니다. 이 매개 변수를 생략하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 검사점 기간을 조정하여 데이터베이스 응용 프로그램의 성능에 미치는 영향을 최소화합니다. *checkpoint_duration*은 고급 옵션입니다.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>검사점 작업 기간에 영향을 주는 요인  
 일반적으로 검사점 작업에 필요한 시간은 기록해야 할 더티 페이지 수에 따라 증가합니다. 다른 응용 프로그램의 성능에 미치는 영향을 최소화하기 위해 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 검사점 작업이 기록하는 빈도를 조정합니다. 기록 빈도를 줄이면 검사점 작업을 완료하는 데 필요한 시간이 늘어납니다. CHECKPOINT 명령에 *checkpoint_duration* 값이 지정되지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수동 검사점에 대해 이 전략을 사용합니다.  
  
 *checkpoint_duration*을 사용하는 경우 성능에 미치는 영향은 더티 페이지 수, 시스템 작업 및 지정한 실제 기간에 따라 다릅니다. 예를 들어 검사점이 120초 내에 정상적으로 완료되는 경우 *checkpoint_duration*을 45초로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본적으로 할당된 리소스보다 더 많은 리소스를 검사점에 할당하게 됩니다. 이와 반대로, *checkpoint_duration*을 180초로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본적으로 할당된 리소스보다 더 적은 리소스를 검사점에 할당하게 됩니다. 일반적으로 *checkpoint_duration*을 짧게 설정하면 검사점에 할당되는 리소스가 증가하고, *checkpoint_duration*을 길게 설정하면 검사점에 할당되는 리소스가 감소합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 가능하면 항상 검사점을 완료하며 CHECKPOINT 문은 검사점이 완료되는 즉시 반환됩니다. 그러므로 지정한 기간보다 빨리 검사점이 완료되거나 지정한 기간보다 오래 실행될 수 있습니다.  
  
##  <a name="Security"></a> 보안  
  
### <a name="permissions"></a>사용 권한  
 CHECKPOINT 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버에게 부여되며, 양도할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [recovery interval 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN&#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
