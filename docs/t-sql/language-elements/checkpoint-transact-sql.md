---
title: "검사점 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 59
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3c0dd607231880ebd7a43b3740eb2cb22b9c195
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 수동 검사점을 생성합니다.  
  
> [!NOTE]  
>  참조에 서로 다른 유형의 데이터베이스 검사점 및 일반적인 검사점 작업에에서 대 한 내용은 [데이터베이스 검사점 &#40; SQL Server &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>인수  
 *checkpoint_duration*  
 수동 검사점을 완료하기 위해 요청된 시간(초)을 지정합니다. 때 *checkpoint_duration* 지정는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 요청 된 기간 내에 검사점을 수행 하려고 합니다. *checkpoint_duration* 유형의 식 이어야 합니다 **int** 하며 0 보다 커야 합니다. 이 매개 변수를 생략하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 검사점 기간을 조정하여 데이터베이스 응용 프로그램의 성능에 미치는 영향을 최소화합니다. *checkpoint_duration* 고급 옵션입니다.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>검사점 작업 기간에 영향을 주는 요인  
 일반적으로 검사점 작업에 필요한 시간은 기록해야 할 더티 페이지 수에 따라 증가합니다. 다른 응용 프로그램의 성능에 미치는 영향을 최소화하기 위해 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 검사점 작업이 기록하는 빈도를 조정합니다. 기록 빈도를 줄이면 검사점 작업을 완료하는 데 필요한 시간이 늘어납니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]제외 수동 검사점에 대 한이 전략을 사용 하 여 한 *checkpoint_duration* CHECKPOINT 명령에 값을 지정 합니다.  
  
 사용 하 여의 성능 영향 *checkpoint_duration* 더티 페이지, 시스템 및 지정한 실제 기간에 해당 활동의 수에 따라 달라 집니다. 검사점 120 초 내에 완료는 일반적으로 지정 하는 예를 들어는 *checkpoint_duration* 45 초로 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본적으로 할당 될 보다 검사점에 더 많은 리소스를 사용할 수 있습니다. 반대로 지정 하는 *checkpoint_duration* 을 180 초로 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본적으로 할당 될 것 보다 적은 리소스를 할당할 수 있습니다. 일반적으로 짧은 *checkpoint_duration* 길게 설정 하면 검사점에 사용 되는 리소스가 증가 합니다 *checkpoint_duration* 검사점에 사용 되는 리소스가 감소 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 가능하면 항상 검사점을 완료하며 CHECKPOINT 문은 검사점이 완료되는 즉시 반환됩니다. 그러므로 지정한 기간보다 빨리 검사점이 완료되거나 지정한 기간보다 오래 실행될 수 있습니다.  
  
##  <a name="Security"></a> 보안  
  
### <a name="permissions"></a>Permissions  
 CHECKPOINT 권한은 기본적으로 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 및 **db_backupoperator** 하지 않으며 고정 데이터베이스 역할 전송할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Recovery interval 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [Shutdown&#40; Transact SQL &#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  

