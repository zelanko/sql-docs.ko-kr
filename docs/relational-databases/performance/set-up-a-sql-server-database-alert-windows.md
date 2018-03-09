---
title: "SQL Server 데이터베이스 경고 설정(Windows) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 447c615f57a71a321a85315cb9de40df5fca8cfc
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>SQL Server 데이터베이스 경고 설정(Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 시스템 모니터를 사용하여 시스템 모니터 카운터가 임계값에 도달했을 때 발생하는 경고를 만들 수 있습니다. 시스템 모니터는 경고에 대한 응답으로 경고 조건을 처리하기 위해 쓰여진 사용자 지정 응용 프로그램과 같은 응용 프로그램을 시작합니다. 예를 들어 교착 상태의 횟수가 지정한 값을 넘어설 때 경고를 발생시킬 수 있습니다. 
  
 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 경고를 정의할 수도 있습니다. 자세한 내용은 [경고](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)를 참조하세요.  
  
## <a name="set-up-a-sql-server-database-alert"></a>SQL Server 데이터베이스 경고 설정  
  
1. **성능** 창의 탐색 트리에서 **성능 로그 및 경고**를 확장합니다.  
  
2. **경고**를 마우스 오른쪽 단추로 클릭한 다음 **새 경고 설정**을 선택합니다.
  
3. **새 경고 설정** 대화 상자에서 새 경고의 이름을 입력한 다음 **확인**을 선택합니다.  
  
4. 새 경고에 대한 대화 상자의 **일반** 탭에서 **설명**을 추가합니다. **추가**를 클릭하여 카운터를 경고에 추가합니다.  
  
     모든 경고에는 적어도 하나의 카운터가 있어야 합니다.  
  
5. **카운터 추가** 대화 상자의 **성능 개체** 목록에서 SQL Server 개체를 선택합니다. **다음에서 카운터 선택** 목록에서 카운터를 선택합니다.  
  
6. 카운터를 경고에 추가하려면 **추가**를 선택합니다. 카운터를 계속 추가하거나 새 경고를 위해 대화 상자로 돌아가려면 **닫기**를 선택합니다.  
  
7. 새 경고 대화 상자에서 **값이 다음일 때 경고 표시**에서 **초과** 또는 **미만**을 선택합니다. 그런 다음 **제한**에 임계값을 입력합니다.  
  
     카운터의 값이 이 임계값보다 크거나 작으면 **초과** 또는 **미만** 선택 여부에 따라 경고가 생성됩니다.  
  
8. **데이터 샘플 간격** 상자에서 샘플 빈도를 설정합니다.  
  
9. **동작** 탭에서 경고가 트리거될 때마다 일어날 동작을 설정합니다.  
  
10. **일정** 탭에서 경고 검사의 시작 및 중지 예약을 설정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 데이터베이스 경고 만들기](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
