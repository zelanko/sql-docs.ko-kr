---
title: 복제 유형 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2fa6d02a8fc501f4b196c175056f18f7a9bff7c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162394"
---
# <a name="types-of-replication"></a>복제 유형
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 분산 응용 프로그램에서 사용할 수 있는 다음 유형의 복제를 제공합니다.  
  
-   트랜잭션 복제. 자세한 내용은 [트랜잭션 복제](transactional/transactional-replication.md)를 참조하세요.  
  
-   병합 복제. 병합 복제에 대한 자세한 내용은 [병합 복제](merge/merge-replication.md)를 참조하세요.  
  
-   스냅숏 복제. 스냅숏 복제에 대한 자세한 내용은 [스냅숏 복제](snapshot-replication.md)를 참조하세요.  
  
 애플리케이션에 대한 복제 유형 선택은 물리적 복제 환경, 복제할 데이터 형식 및 양, 데이터가 구독자에서 업데이트되는지 여부를 포함한 여러 요인에 따라 달라집니다. 물리적 환경에는 복제와 관련된 컴퓨터 수 및 위치와 이러한 컴퓨터가 클라이언트(워크스테이션, 랩톱 또는 핸드헬드 디바이스)인지 또는 서버인지 여부가 포함됩니다.  
  
 일반적으로 각 복제 유형은 게시자와 구독자 간에 게시된 개체의 초기 동기화로 시작합니다. 이러한 초기 동기화는 게시에 의해 지정된 모든 개체 및 데이터의 복사본인 *스냅숏*이 있는 복제로 수행할 수 있습니다. 스냅숏은 생성된 후 구독자로 배달됩니다. 스냅숏 복제만 필요한 애플리케이션도 있고, 시간에 따라 증분 방식으로 후속 데이터 변경 내용을 구독자로 보내야 하는 애플리케이션도 있습니다. 또한 일부 애플리케이션에서는 변경 내용을 구독자에서 게시자로 다시 보내야 합니다. 트랜잭션 복제 및 병합 복제는 이러한 유형의 애플리케이션에 대한 옵션을 제공합니다.  
  
 스냅숏 복제에 대한 데이터 변경 내용은 추적되지 않으며 스냅숏이 적용될 때마다 이 스냅숏은 기존 데이터를 완전히 덮어씁니다. 트랜잭션 복제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 로그를 통해 변경 내용을 추적하고 병합 복제는 트리거 및 메타데이터 테이블을 통해 변경 내용을 추적합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 개요](agents/replication-agents-overview.md)  
  
  
