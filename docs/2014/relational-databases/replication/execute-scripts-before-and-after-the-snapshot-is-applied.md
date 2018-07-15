---
title: 스냅숏 적용 전후에 스크립트 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
- scripts [SQL Server replication]
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fde608be7281ca66856f63db3a2626863c1a30f1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320053"
---
# <a name="execute-scripts-before-and-after-the-snapshot-is-applied"></a>스냅숏 적용 전후에 스크립트 실행
  스냅숏 적용 전후에 구독자에서 스크립트가 실행되도록 지정할 수 있습니다. 각 구독자에서 로그인과 스키마(개체 소유자)를 만드는 작업 등 다양한 작업에 스크립트를 사용할 수 있습니다.  
  
 사용자가 각 스크립트에 대한 파일 위치를 지정하면 스냅숏 에이전트는 스냅숏 처리가 발생할 때마다 해당 스크립트 파일을 현재 스냅숏 폴더로 복사합니다. 배포 에이전트 또는 병합 에이전트는 스냅숏을 적용할 때 복제된 모든 개체 스크립트보다 먼저 프리 스냅숏 스크립트를 실행합니다. 배포 에이전트 또는 병합 에이전트는 복제된 다른 개체 스크립트 및 데이터가 모두 적용된 후에 포스트 스냅숏 스크립트를 실행합니다. 스냅숏 응용 프로그램이 완료되고 스크립트 파일이 성공적으로 실행되면 스크립트 파일은 구독자의 작업 디렉터리에서 제거됩니다.  
  
 스크립트는 **sqlcmd** 유틸리티를 시작하여 실행합니다. 스크립트를 배포하기 전에 **sqlcmd** 로 스크립트를 실행하여 예상된 대로 실행되는지 확인합니다. 스냅숏 적용 전후에 실행되는 스크립트의 내용은 반복 가능해야 합니다. 예를 들어 스크립트로 테이블을 만들려면 먼저 테이블이 존재하는지 확인하고 테이블이 존재하면 적절한 조치를 취해야 합니다. 스크립트가 이미 적용된 구독을 다시 초기화할 필요가 있다면 다시 초기화하는 중에 새 스냅숏이 적용될 때 스크립트도 다시 적용될 것이기 때문에 스크립트는 반복 가능해야 합니다.  
  
 스냅숏 파일을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 파일 형식으로 압축하는 중이면 스크립트도 압축되어 CAB 파일 내에 위치합니다. 압축 스냅숏 파일을 구독자로 전송하고 구독자의 작업 디렉터리로 압축을 풀면 프리 스냅숏 스크립트로 표시된 모든 스크립트가 실행됩니다. 마찬가지로 모든 포스트 스냅숏 스크립트도 압축이 풀리고 스냅숏 적용의 마지막 단계로 구독자에서 실행됩니다.  
  
 **스냅숏 적용 전후에 스크립트를 실행하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [방법: 스냅숏 적용 전후에 스크립트 실행\(SQL Server Management Studio\)](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   복제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍: [스냅숏 속성 구성&#40;복제 TRANSACT-SQL 프로그래밍&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>관련 항목  
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [스냅숏 옵션](snapshot-options.md)  
  
  
