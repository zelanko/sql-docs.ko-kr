---
title: 정책 예약 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8becd7ad30acf1ea2a63feae4760091aede70c06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033505"
---
# <a name="schedule-the-policies"></a>정책 예약
  이 태스크에서는 이전 태스크에서 가져온 최선의 구현 방법 정책을 예약합니다.  
  
### <a name="to-schedule-the-best-practices-policies"></a>최선의 구현 방법 정책을 예약하려면  
  
1.  개체 탐색기에서 **관리**, **정책 관리**, **정책을 차례로**확장 하 고 모범 사례 정책을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
    > [!NOTE]  
    >  또는 모범 사례와 관련 된 정책을 쉽게 확인 하 고 모범 사례 범주를 정렬 하려면 **관리**, **정책 관리**를 차례로 확장 한 다음 **정책**을 클릭 합니다. **보기** 메뉴에서 **개체 탐색기 정보**를 클릭합니다. **개체 탐색기 세부 정보** 창에서 **범주** 제목을 클릭 하 여 범주별로 정책을 정렬 합니다. 최선의 구현 방법 정책에는 **Microsoft 모범 사례**접두사가 있습니다. 구성 하려는 정책을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
2.  **정책 열기** 대화 상자의 **일반** 페이지에 있는 **평가 모드** 목록에서 **일정을**클릭 합니다.  
  
3.  **일정** 상자 옆의 **선택** 을 클릭 하 여 기존 일정을 지정 하거나 **새로** 만들기를 클릭 하 여 새 일정을 만듭니다.  
  
4.  일정을 구성한 후 페이지 맨 위 근처에서 **사용** 확인란을 선택 하 여 예약 된 정책을 사용 하도록 설정할 수 있습니다.  
  
5.  예약할 각 정책에 대해 1-4단계를 반복합니다.  
  
    > [!NOTE]  
    >  예약된 정책 실행 이후 평가 결과를 보려면 대상 인스턴스에 대한 정책 기록 로그를 엽니다. 로그를 열려면 **정책 관리**를 마우스 오른쪽 단추로 클릭 한 다음 **기록 보기**를 클릭 합니다.  
  
## <a name="summary"></a>요약  
 예약된 정책을 단일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행하도록 구성했습니다. 예약된 정책을 여러 인스턴스에 배포하려면 이 자습서의 다음 태스크를 계속 진행합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [여러 인스턴스에 예약된 정책 배포](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
