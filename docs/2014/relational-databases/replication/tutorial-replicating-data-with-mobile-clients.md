---
title: '자습서: 모바일 클라이언트와의 데이터 복제 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5a95b157761cc9a61d09271b5e081a65cd45998
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056243"
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>자습서: 모바일 클라이언트와의 데이터 복제
  복제는 가끔 연결되는 중앙 서버와 모바일 클라이언트간에 데이터를 이동할 때 발생하는 문제를 해결하는 좋은 방법입니다. 복제 마법사를 사용하면 복제 토폴로지를 쉽게 구성하고 관리할 수 있습니다. 이 자습서에서는 모바일 클라이언트에 대해 복제 토폴로지를 구성하는 방법에 대해 설명합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 각 사용자가 고유하게 필터링된 데이터의 하위 집합을 얻을 수 있도록 병합 복제를 사용하여 중앙 데이터베이스의 데이터를 여러 모바일 사용자에게 게시합니다. 첫 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 게시를 만드는 방법을 보여 줍니다. 이후의 단원에서는 구독을 만들고 이를 동기화하는 방법을 보여 줍니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다. 이 자습서를 시작하려면 이전 자습서인 [자습서: 복제용 서버 준비](tutorial-preparing-the-server-for-replication.md)를 완료해야 합니다.  
  
 이 자습서를 사용하려면 시스템에 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   게시자 서버(원본)  
  
    -   Express( [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 또는[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 제외한 [!INCLUDE[ssEW](../../includes/ssew-md.md)]의 모든 버전. 이러한 버전은 복제 게시자가 될 수 없습니다.  
  
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
-   구독자 서버(대상)  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]을 제외한 [!INCLUDE[ssEW](../../includes/ssew-md.md)]의 모든 버전. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 을 지원하지 않습니다.  
  
    > [!NOTE]  
    >  복제는 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 설치되지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 sysadmin 고정 서버 역할의 멤버인 로그인을 사용하여 게시자 및 구독자에 연결해야 합니다.  
  
 **이 자습서에 소요되는 예상 시간: 30분**  
  
## <a name="lessons-in-this-tutorial"></a>이 자습서의 단원  
  
-   [1단원: 병합 복제를 사용하여 데이터 게시](lesson-1-publishing-data-using-merge-replication.md)  
  
-   [2단원: 병합 게시에 대한 구독 만들기](lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
 [자습서 시작](merge/merge-replication.md)  
  
## <a name="see-also"></a>관련 항목  
 [복제 프로그래밍 개념](concepts/replication-programming-concepts.md)  
  
  
