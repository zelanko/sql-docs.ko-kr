---
title: 동기화 중 스크립트 실행(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0be050105f1c848201ea2b0cc3780234594c3ae6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184904"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>동기화 중 스크립트 실행(복제 Transact-SQL 프로그래밍)
  복제는 트랜잭션 게시 및 병합 게시 구독자의 요청 시 스크립트 실행을 지원합니다. 이 기능은 복제 작업 디렉터리에 스크립트를 복사한 다음 **sqlcmd** 를 사용하여 구독자에서 스크립트를 적용합니다. 구독자의 스크립트를 트랜잭션 게시에 적용할 때 오류가 발생하면 기본적으로 배포 에이전트가 중지됩니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 실행되도록 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 지정할 수 있습니다.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>스냅숏, 트랜잭션 또는 병합 게시의 모든 구독자에 대해 실행되도록 스크립트를 지정하려면  
  
1.  요청 시 실행되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 작성 및 테스트합니다.  
  
2.  게시에 대한 스냅숏 에이전트가 액세스할 수 있는 위치에 스크립트 파일을 저장합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addscriptexec&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql)를 실행합니다. **@publication**, **@scriptfile**에 2단계에서 만든 전체 UNC 경로를 포함하는 스크립트 파일의 이름, **@skiperror**에 다음 값 중 하나를 지정합니다.  
  
    -   **0** - 오류가 발생하면 스크립트 실행이 중지됩니다.  
  
    -   **1** - 오류가 발생하면 로그에 기록되고 스크립트는 계속 실행됩니다.  
  
4.  지정된 스크립트는 구독을 동기화하기 위해 다음에 에이전트가 실행될 때 각 구독자에서 실행됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 동기화](synchronize-data.md)  
  
  
