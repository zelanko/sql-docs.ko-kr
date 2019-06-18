---
title: 데이터 동기화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], about synchronization
- merge replication synchronization [SQL Server replication]
- scripts [SQL Server replication], synchronization and
- synchronization [SQL Server replication]
- snapshot replication [SQL Server], synchronization
- transactional replication, synchronization
- subscriptions [SQL Server replication], synchronizing
- on demand script execution
- replication [SQL Server], synchronization
- scripts [SQL Server replication]
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 15f4d85d117b5af09b0f67ef788364be6adad810
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745494"
---
# <a name="synchronize-data"></a>데이터 동기화
  데이터 동기화란 초기 스냅숏이 구독자에 적용된 후 게시자와 구독자 간에 데이터 및 스키마 변경 내용이 전파되는 프로세스를 말합니다. 동기화는 다음과 같은 방식으로 발생할 수 있습니다.  
  
-   계속 - 트랜잭션 복제에 일반적임  
  
-   요청 시 - 병합 복제에 일반적임  
  
-   일정대로 - 스냅숏 복제에 일반적임  
  
 구독이 동기화되면 사용하는 복제 유형에 따라 다른 프로세스가 발생합니다.  
  
-   스냅숏 복제. 동기화란 배포 에이전트가 구독 데이터베이스의 스키마와 데이터가 게시 데이터베이스와 일치하도록 구독자에 스냅숏을 다시 적용하는 것을 말합니다.  
  
     게시자에서 데이터와 스키마를 수정한 경우 수정 내용을 구독자에 전파하려면 새 스냅숏을 생성해야 합니다.  
  
-   트랜잭션 복제. 동기화란 배포 에이전트가 업데이트, 삽입, 삭제 및 기타 변경 내용을 배포 데이터베이스에서 구독자로 전송하는 것을 말합니다.  
  
-   병합 복제. 동기화란 병합 에이전트가 변경 내용을 구독자에서 게시자로 업로드한 다음 게시자에서 구독자로 변경 내용을 다운로드하는 것을 말합니다. 충돌이 발생할 경우 이를 감지하여 해결합니다. 데이터는 일치되고 게시자와 모든 구독자는 결국 같은 데이터 값을 갖게 됩니다. 충돌이 감지되고 해결될 때 일부 사용자가 커밋한 작업은 사용자가 정의한 정책에 따라 충돌을 해결하도록 변경됩니다.  
  
 스냅숏 게시는 동기화가 발생할 때마다 구독자에서 스키마를 완전히 새로 고치므로 모든 스키마 변경 내용이 구독자에 적용됩니다. 트랜잭션 복제 및 병합 복제 또한 가장 일반적인 스키마 변경을 지원합니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
 밀어넣기 구독을 동기화하려면 [밀어넣기 구독 동기화](synchronize-a-push-subscription.md)를 참조하십시오.  
  
 끌어오기 구독을 동기화하려면 [끌어오기 구독 동기화](synchronize-a-pull-subscription.md)를 참조하십시오.  
  
 동기화 일정을 설정하려면 [동기화 일정 지정](specify-synchronization-schedules.md)을 참조하십시오.  
  
 **동기화 충돌을 보고 해결하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [병합 게시에 대한 데이터 충돌 보기 및 해결&#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## <a name="executing-code-during-synchronization"></a>동기화 중 코드 실행  
 복제는 동기화하는 동안 코드를 실행하는 두 가지 방법을 지원합니다.  
  
-   요청 시 스크립트 실행은 트랜잭션 복제와 병합 복제에 대해 지원됩니다. 요청 시 스크립트 실행을 사용하면 동기화하는 동안 SQL 스크립트가 실행되도록 지정할 수 있습니다. 스크립트는 구독자에 복사된 다음 동기화 프로세스 시작 시 **sqlcmd** 를 사용하여 실행됩니다. 복제된 변경 내용이 구독자에 적용될 때 스크립트를 통해 이러한 변경 내용에 액세스할 수 없습니다. 자세한 내용은 [동기화 중 스크립트 실행&#40;복제 Transact-SQL 프로그래밍&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)을 참조하세요.  
  
-   비즈니스 논리 처리기는 병합 복제에 대해 지원됩니다. 비즈니스 논리 처리기 프레임워크를 사용하면 병합 동기화 과정 동안 호출되는 관리 코드 어셈블리를 작성할 수 있습니다. 이 어셈블리에는 동기화 중 데이터 변경, 충돌, 오류 등의 여러 상황에 응답할 수 있는 비즈니스 논리가 포함되어 있습니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [병합 복제 충돌 감지 및 해결](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
