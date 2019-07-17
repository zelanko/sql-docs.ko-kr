---
title: 기타 복제 업그레이드 문제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd8ae8bb1080d92bb6a4ad1ba982f1dffc6d51f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093640"
---
# <a name="other-replication-upgrade-issues"></a>기타 복제 업그레이드 문제
  이 항목에서는 업그레이드 관리자가 보고하지 않는 몇 가지 업그레이드 문제에 대해 설명합니다.  
  
## <a name="versions-supported"></a>지원되는 버전  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복제된 데이터베이스를 업그레이드할 수 있도록 지원합니다. 따라서 노드 업그레이드 중에 다른 노드의 작업을 중지할 필요가 없으며 한 토폴로지 내에서 지원되는 버전과 관련된 규칙만 잘 지키면 됩니다.  
  
 서로 다른 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 복제하는 경우 가장 오래된 버전의 기능으로 제한되는 경우가 많습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크상 저장소 형식은 64비트 및 32비트 환경에서 동일하므로 복제 토폴로지가 32비트 환경에서 실행되는 서버 인스턴스와 64비트 환경에서 실행되는 서버 인스턴스를 결합할 수 있습니다.  
  
 모든 유형의 복제에서 배포자 버전은 게시자 버전과 같거나 그 이후 버전이어야 합니다. 배포자는 게시자와 동일한 인스턴스로 실행되는 경우가 많습니다.  
  
 트랜잭션 복제의 경우 트랜잭션 게시에 대한 구독자는 게시자의 두 가지 버전 중 어느 버전이든 가능합니다.  
  
 병합 복제의 경우 병합 게시에 대한 구독자는 게시자 버전과 같거나 이전 버전일 수 있습니다.  
  
## <a name="merge-replication-batches-changes"></a>병합 복제 일괄 처리 변경 내용  
 성능을 높이기 위해 병합 에이전트에서 수행된 변경 내용이 일괄 처리되므로 단일 문에서 둘 이상의 행을 삽입, 업데이트 또는 삭제할 수 있습니다. 게시 또는 구독 데이터베이스의 게시된 테이블에 트리거가 있을 경우 해당 트리거에서 다중 행 삽입, 업데이트 및 삭제를 처리할 수 있습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "DML 트리거에 대한 다중 행 고려 사항"을 참조하십시오.  
  
## <a name="activex-control-changes"></a>ActiveX 컨트롤 변경 내용  
 복제 ActiveX 컨트롤에서 변경된 사항은 다음과 같습니다.  
  
-   모든 ActiveX 컨트롤은 스크립팅 및 초기화에 안전하지 않은 것으로 표시됩니다.  
  
-   스냅샷 ActiveX 컨트롤은 삭제되었습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하거나 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 스냅숏을 만들고 관리할 수 있습니다. 자세한 내용은 항목을 참조 하세요. "방법: 만들기 및 Apply the Initial Snapshot ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) "및" 방법: 초기 스냅숏 (복제 TRANSACT-SQL 프로그래밍) 만들기 "에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인입니다.  
  
-   분산 ActiveX 컨트롤 및 병합 ActiveX 컨트롤은 이후에는 지원되지 않습니다. RMO(복제 관리 개체)를 사용한 관리 코드 응용 프로그램에 비슷한 기능이 제공됩니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "구독 동기화(RMO 프로그래밍)"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [복제 업그레이드 문제](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
