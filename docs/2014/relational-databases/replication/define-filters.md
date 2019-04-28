---
title: 필터 정의 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7b82b3450727d36a36186453e366625ebecbde2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721387"
---
# <a name="define-filters"></a>필터 정의
  **필터 정의** 대화 상자를 사용하여 필터를 정의한 다음 데이터 충돌에 적용하여 충돌의 하위 집합을 표로 볼 수 있습니다. 필터를 정의하려면 **연산자** 드롭다운 목록 상자에서 연산자를 선택하고 값을 입력합니다. 예를 들어 충돌 시 서버 **ReplTest1**의 변경 내용이 무시되는 충돌만 표시하려면 **연산자** 드롭다운 목록 상자에서 **같음** 을 선택하고 첫 번째 **값** 열에 **ReplTest1** 을 입력합니다.  
  
## <a name="options"></a>변수  
 **연산자**  
 **작거나 같음**등의 필터에 대한 연산자를 선택합니다.  
  
 **ReplTest1**  
 필터 값을 입력합니다. 대부분의 연산자는 첫 번째 **값** 열에만 값을 입력하면 되지만 **사이** 및 **사이에 있지 않음** 연산자는 두 **값** 열에 값을 모두 입력해야 합니다.  
  
 **지우기**  
 이 단추를 클릭하여 이전에 정의한 필터를 모두 지울 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 복제 충돌 뷰어&#40;병합 복제&#41;](microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft 복제 충돌 뷰어&#40;트랜잭션 복제&#41;](microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
