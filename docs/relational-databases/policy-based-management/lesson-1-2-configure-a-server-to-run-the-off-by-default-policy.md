---
title: "Off By Default 정책을 실행하도록 서버 구성 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b92cd0c1cebaacca432cb45422682f12423f67ea
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-1-2---configure-a-server-to-run-the-off-by-default-policy"></a>1-2단원 - Off By Default 정책을 실행하도록 서버 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이제 Off By Default라는 정책이 만들어졌습니다. 이 태스크에서는 서버가 이 정책의 요구 사항을 준수하는지 여부를 확인합니다.  
  
### <a name="to-run-the-off-by-default-policy"></a>Off By Default 정책을 실행하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **평가**를 클릭합니다.  
  
2.  **정책 평가** 대화 상자에서는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 파일에서 정책을 선택할 수 있습니다. 이 단계를 위해서 **원본** 을 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스로 설정해 둡니다.  
  
3.  **정책** 섹션에서 **Off By Default** 정책을 선택합니다.  
  
4.  서버가 정책을 준수하는지 여부를 확인하려면 **평가**를 클릭합니다.  
  
5.  **이 정책을 준수하는 경우** 결과 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 영역에 확인 표시가 있는 녹색 원이 나타납니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 정책을 준수하지 않는 경우 X 표시가 있는 빨간색 원이 나타납니다.  
  
6.  오류가 발생할 경우 **대상 정보** 영역의 **메시지** 열에서 추가 정보를 볼 수 있습니다. **메시지** 열에서 **보기** 를 클릭하여 검사한 각 패싯 속성에 대한 검사 결과를 포함하는 보고서를 볼 수 있습니다.  
  
7.  정책 설명이 페이지 아래쪽에 표시되고 **추가 도움말** 섹션에서 정책에 대해 구성한 하이퍼링크를 표시합니다. 메시지 하이퍼링크를 클릭하여 정책을 만들 때 지정한 웹 페이지를 엽니다.  
  
8.  브라우저를 닫은 다음 **결과 자세히 보기** 대화 상자를 닫습니다.  
  
9. 서버가 정책을 준수하지 않고, 데이터베이스 메일을 사용하지 않으려는 경우 **평가 결과** 페이지에서 **적용** 을 클릭합니다.  
  
10. **결과 자세히 보기** 대화 상자와 **정책 평가** 대화 상자를 모두 닫습니다.  
  
## <a name="next-lesson"></a>다음 단원  
[2단원: 명명 표준 정책 만들기 및 적용](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
