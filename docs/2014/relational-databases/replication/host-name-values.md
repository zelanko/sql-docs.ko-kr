---
title: HOST_NAME 값 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8f7f1304b0d72cf59467aee16c04481fbd51ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721191"
---
# <a name="hostname-values"></a>HOST_NAME 값
  매개 변수가 있는 필터가 포함된 병합 게시는 SUSER_SNAME() 함수 및/또는 HOST_NAME() 함수를 사용하여 데이터를 필터링합니다. 함수는 새 게시 마법사 또는 **게시 속성** 대화 상자에서 지정합니다.  
  
 기본적으로 HOST_NAME() 함수는 게시자에 연결하는 컴퓨터 이름을 반환합니다. 매개 변수가 있는 필터를 사용할 경우 이 마법사 페이지에서 값을 입력하여 이 값을 재정의하는 것이 일반적입니다. 그러면 HOST_NAME() 함수는 컴퓨터 이름 대신 사용자가 지정한 값을 반환합니다. 자세한 내용은 [매개 변수가 있는 행 필터](merge/parameterized-filters-parameterized-row-filters.md)의 “HOST_NAME() 값 재정의”를 참조하세요.  
  
> [!NOTE]  
>  HOST_NAME()을 재정의할 경우 HOST_NAME() 함수에 대한 모든 호출은 사용자가 지정한 값을 반환합니다. 다른 애플리케이션이 컴퓨터 이름을 반환하는 HOST_NAME()에 종속되지 않아야 합니다.  
  
## <a name="options"></a>변수  
 **구독 속성**  
 **HOST_NAME 값** 열에 각 구독자에 대한 값을 입력하거나 구독자 컴퓨터의 이름인 기본값을 적용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [끌어오기 구독 속성 보기 및 수정](view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](view-and-modify-push-subscription-properties.md)   
 [HOST_NAME&#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)   
 [게시 구독](subscribe-to-publications.md)  
  
  
