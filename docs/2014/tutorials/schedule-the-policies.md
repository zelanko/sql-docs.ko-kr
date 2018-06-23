---
title: 정책 예약 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 99c6e3a4eacfea76ff16ea266d38f2087c088f33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088972"
---
# <a name="schedule-the-policies"></a>정책 예약
  이 태스크에서는 이전 태스크에서 가져온 최선의 구현 방법 정책을 예약합니다.  
  
### <a name="to-schedule-the-best-practices-policies"></a>최선의 구현 방법 정책을 예약하려면  
  
1.  개체 탐색기에서 확장 **관리**를 확장 하 고 **정책 관리**, 확장 **정책**는 최선의 구현 방법 정책을 마우스 오른쪽 단추로 클릭 한 다음 클릭  **속성**합니다.  
  
    > [!NOTE]  
    >  대신, 모범 사례와 연결 된 어떤 정책이 쉽게 확인할 수와 가장 적합 한 정렬 하려면 구현 방법 범주를 **관리**, 확장 **정책 관리**, 클릭하고**정책**합니다. **보기** 메뉴에서 **개체 탐색기 정보**를 클릭합니다. 에 **개체 탐색기 정보** 창에서 클릭 된 **범주** 머리글을 범주별으로 정책을 정렬할 합니다. 최선의 구현 방법 정책을 접두사가 **Microsoft Best Practices**합니다. 구성 하 고 클릭 하려는 정책을 마우스 오른쪽 단추로 **속성**합니다.  
  
2.  에 **일반** 의 페이지는 **정책 열기** 대화 상자는 **평가 모드** 목록에서 클릭 **일정에 따라**합니다.  
  
3.  옆에 **일정** 상자를 클릭 **선택** 하 여 기존 일정을 지정 하거나 클릭 **새로** 새 일정을 만듭니다.  
  
4.  일정을 구성한 후 선택할 수 있습니다는 **Enabled** 예약 된 정책을 사용 하는 페이지의 위쪽 확인란 합니다.  
  
5.  예약할 각 정책에 대해 1-4단계를 반복합니다.  
  
    > [!NOTE]  
    >  예약된 정책 실행 이후 평가 결과를 보려면 대상 인스턴스에 대한 정책 기록 로그를 엽니다. 로그를 열려면 마우스 오른쪽 단추로 클릭 **정책 관리**, 클릭 하 고 **기록 보기**합니다.  
  
## <a name="summary"></a>요약  
 예약된 정책을 단일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행하도록 구성했습니다. 예약된 정책을 여러 인스턴스에 배포하려면 이 자습서의 다음 태스크를 계속 진행합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [여러 인스턴스에 예약된 정책 배포](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  