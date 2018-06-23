---
title: 게시 속성, 데이터 파티션 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fe5c3417d20656c207bcdddea97b8cb998d5050f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089034"
---
# <a name="publication-properties-data-partitions"></a>게시 속성, 데이터 파티션
  **게시 속성** 대화 상자의 **데이터 파티션** 페이지를 사용하여 매개 변수가 있는 필터링을 사용하는 병합 게시를 위한 데이터 파티션을 정의할 수 있습니다. 파티션을 정의하고 나면 이들 파티션에 대한 스냅숏을 생성하여 구독자의 연결 속성(로그인 및/또는 컴퓨터 이름)을 기준으로 다양한 구독자에 대한 각기 다른 초기 데이터 집합을 제공할 수 있습니다. 또한 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅숏을 가지고 있지 않은 경우 스냅숏 배달 및 생성을 요청할 수 있도록 선택할 수 있습니다. 자세한 내용은 [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **추가**  
 파티션을 정의하려면 **추가** 를 클릭합니다. **데이터 파티션 추가** 대화 상자에서 **HOST_NAME()** 및/또는 **SUSER_SNAME()** 에 대한 값을 지정하고 스냅숏을 새로 고칠 일정을 정의합니다.  
  
 **편집**  
 표에서 기존 파티션을 선택하고 **편집** 을 클릭하여 파티션을 편집합니다.  
  
 **Delete**  
 표에서 기존 파티션을 선택하고 **삭제** 를 클릭하여 파티션을 삭제합니다.  
  
 **선택한 스냅숏 지금 생성**  
 표에서 하나 이상의 파티션을 선택하고 **선택한 스냅숏 지금 생성** 을 클릭하여 이러한 파티션에 대한 스냅숏을 생성합니다.  
  
 **기존 스냅숏 정리**  
 표에서 하나 이상의 파티션을 선택하고 **기존 스냅숏 정리** 를 클릭하여 이러한 파티션에 대한 스냅숏을 정리합니다.  
  
 **새 구독자가 동기화할 때 필요한 경우 자동으로 파티션 정의 및 스냅숏 생성**  
 구독자가 스냅숏 생성 및 적용을 요청할 수 있도록 할 경우 이 옵션을 선택합니다. 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅숏을 가지고 있지 않은 경우 이 옵션이 필요할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Publication](publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](publish/publish-data-and-database-objects.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  