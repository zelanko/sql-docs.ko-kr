---
title: "멤버 수정 기록 롤백 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42b58095bac7ea8532e12a0683d0fda6806156a3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="rollback-member-revision-history-master-data-services"></a>멤버 수정 기록 롤백(Master Data Services)
  멤버 수정 기록은 멤버를 변경할 때마다 기록됩니다. 멤버 수정 기록을 이전 버전으로 롤백할 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
  
-   선택한 멤버의 특성 하나 이상을 업데이트할 권한이 있어야 합니다. 수정 기록을 롤백하면 업데이트할 수 있는 모든 특성 값이 이전 버전 값으로 롤백됩니다.  
  
-   엔터티의 트랜잭션 로그 유형이 멤버일 때만 수정 기록을 사용할 수 있습니다.  
  
 **멤버 수정 기록을 롤백하려면**  
  
1.  마스터 데이터 관리자에서 탐색기를 클릭합니다.  
  
2.  롤백할 엔터티와 멤버를 선택합니다.  
  
3.  **기록 보기**를 클릭합니다.  
  
4.  롤백할 수정을 선택하고 **롤백**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [멤버 수정 기록&#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [엔터티 트랜잭션 로그 유형 &#40; 변경 Master Data services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
