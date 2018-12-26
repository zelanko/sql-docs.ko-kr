---
title: MSSQLSERVER_8525 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0e254e38eabc62ab3e11e7d8ab1a3396c465470
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118693"
---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8525|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|분산 트랜잭션이 완료되었습니다. 이 세션을 새 트랜잭션이나 NULL 트랜잭션에 참여하게 하십시오.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 DTC(Distributed Transaction Coordinator)를 사용하기 위한 프로그래밍 모델에서는 응용 프로그램을 명시적으로 분산 트랜잭션에 참여시키고 분산 트랜잭션에서 제거해야 합니다.  
  
 이 오류는 다음과 같은 4가지 조건이 만족되면 발생합니다.  
  
-   애플리케이션이 분산 트랜잭션에 참여했습니다.  
  
-   어떤 이유로 인해 트랜잭션이 종료되어 커밋되거나 롤백되었습니다.  
  
-   사용자 애플리케이션이 명시적으로 분산 트랜잭션에서 제거되지 않았거나 명시적으로 새로운 분산 트랜잭션에 참여하지 않았습니다.  
  
-   애플리케이션이 기존 분산 트랜잭션에서 제거하거나 새로운 분산 트랜잭션에 참여하는 작업 이외의 트랜잭션 작업(예: 쿼리 실행 또는 로컬 트랜잭션 시작)을 수행하려고 합니다.  
  
 오류 상태 1은 애플리케이션이 로컬 트랜잭션을 만드는 작업을 수행하는 경우 사용되며 상태 2는 애플리케이션이 바운드 세션에 참여하려고 하는 경우 사용됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 애플리케이션이 분산 트랜잭션에 참여한 다음에는 해당 애플리케이션을 명시적으로 분산 트랜잭션에서 제거하거나 다른 분산 트랜잭션에 참여시켜야 합니다. 이렇게 하면 응용 프로그램이 이전에 참여한 트랜잭션에서 암시적으로 제거됩니다. 분산 트랜잭션에서 제거하거나 분산 트랜잭션에 참여시키기 위한 정확한 구문은 애플리케이션에 대한 프로그래밍 인터페이스 매뉴얼을 참조하십시오.  
  
  
