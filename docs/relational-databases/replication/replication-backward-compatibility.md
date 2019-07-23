---
title: 복제의 이전 버전과의 호환성 | Microsoft 문서
ms.custom: ''
ms.date: 03/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, backward compatibility
- backward compatibility [SQL Server replication]
- merge replication backward compatibility [SQL Server replication]
- replication [SQL Server], backward compatibility
- backward compatibility [SQL Server], replication
- snapshot replication [SQL Server], backward compatibility
- compatibility [SQL Server replication]
ms.assetid: 091c51dc-8b32-4b4f-847e-b317456c8394
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b21412bfb6555dbe9c45d411f0b1e7292e79e2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046706"
---
# <a name="replication-backward-compatibility"></a>복제의 이전 버전과의 호환성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

업그레이드하는 경우 또는 복제 토폴로지에 둘 이상의 SQL Server 버전이 있는 경우 이전 버전과의 호환성을 이해하는 것이 중요합니다. 

일반 규칙은 다음과 같습니다. 

-   배포자는 게시자 버전 이상인 모든 버전일 수 있습니다. 많은 경우에 배포자는 게시자와 동일한 인스턴스에 있습니다.    
-   게시자는 배포자 버전 이하인 모든 버전일 수 있습니다.    
-   구독자 버전은 게시 유형에 따라 달라집니다.    
    - 트랜잭션 게시에 대한 구독자는 게시자의 두 가지 버전 중 어떤 버전이든 될 수 있습니다. 예를 들어 SQL Server 2012(11.x) 게시자에는 SQL Server 2014(12.x) 및 SQL Server 2016(13.x) 구독자가 있을 수 있으며, SQL Server 2016(13.x) 게시자에는 SQL Server 2014(12.x) 및 SQL Server 2012(11.x) 구독자가 있을 수 있습니다.     
    - 병합 게시에 대한 구독자는 버전 수명 주기 지원 주기에 따라 지원되는 게시자 버전과 같거나 낮은 모든 버전이 될 수 있습니다.  


## <a name="replication-matrix"></a>복제 매트릭스
[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]


## <a name="additional-resources"></a>추가 리소스
 [SQL Server 복제에서 사용되지 않는 기능](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
 이전 버전과의 호환성을 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 유지되었지만 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 제거될 복제 기능입니다.  
  
 [SQL Server 복제의 주요 변경 내용](../../relational-databases/replication/breaking-changes-in-sql-server-replication.md)  
 애플리케이션을 변경해야 할 수도 있는 복제 기능 변경 내용 

 [복제된 데이터베이스 업그레이드](../../database-engine/install-windows/upgrade-replicated-databases.md)  
 복제 토폴로지에 참여하는 SQL Server를 업그레이드할 때 고려해야 할 단계 및 고려 사항입니다. 
  
  
