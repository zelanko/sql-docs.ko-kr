---
title: "사용자 지정 인덱스(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 2347f26d041c15142487420440a470f87a822e3e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="custom-index-master-data-services"></a>사용자 지정 인덱스(Master Data Services)
  사용자 지정 인덱스는 엔터티에서 하나의 속성(단일 인덱스) 또는 속성 목록(복합 인덱스)에 대한 비클러스터형 인덱스를 생성합니다. 일반적으로 인덱스는 쿼리 프로세스의 성능을 향상시킵니다. SQL Server 인덱스에 대한 자세한 내용은 [인덱스](../relational-databases/indexes/indexes.md)를 참조하세요.  
  
## <a name="type-of-indexes"></a>인덱스 유형  
 각 엔터티에 대하여 다음과 같은 여러 사용자 지정 인덱스를 생성할 수 있습니다.  
  
-   고유 인덱스  
  
-   고유하지 않은 인덱스  
  
 고유 인덱스는 인덱싱된 열에 중복 값이 포함되어 있는지 확인합니다. 복합 고유 인덱스의 경우 인덱스는 선택한 속성 목록에서 각 값 조합이 고유한지 확인합니다. 선택한 속성에 대하여 중복 값이 존재하는 경우 고유 인덱스가 생성될 수 없습니다.  
  
## <a name="rules"></a>규칙  
 사용자 지정 인덱스(고유 및 비고유)에는 다음 규칙이 적용됩니다.  
  
-   사용자 지정 인덱스를 만들려면 하나 이상의 속성을 선택해야 합니다.  
  
-   속성 목록이 동일하고 고유성 플래그가 있는 인덱스를 다른 인덱스로 저장하려는 경우 해당 인덱스를 저장할 수 없습니다. 오류가 표시됩니다.  
  
    > [!NOTE]  
    >  MDS는 특정 속성에 대한 인덱스를 자동으로 생성합니다(예: DBA 및 코드). 즉, 이러한 속성 중 하나를 포함하고 다른 속성을 포함하지 않는 다른 인덱스를 만들 수 없습니다.  
  
-   다른 인덱스에 하나 이상의 서로 다른 속성이 있는 경우 하나 이상의 사용자 지정 인덱스에 속성이 포함될 수 없습니다. 그렇지 않은 경우 인덱스는 동일합니다.  
  
-   여러 속성 또는 대규모 속성을 포함하는 인덱스를 생성하고 선택한 속성의 전체 크기가 최대 인덱스 키 크기(900 바이트)를 초과하는 경우 인덱스를 저장할 수 없습니다.  
  
-   사용자 지정 인덱스는 파일 속성을 제외한 리프 멤버 속성에서 생성될 수 있습니다.  
  
-   사용자 지정 인덱스에 포함된 속성을 삭제하려면 다음을 수행합니다.  
  
    -   한 속성에서만 인덱스가 생성된 경우(단일 인덱스) 속성 및 인덱스 모두 삭제됩니다.  
  
    -   둘 이상의 속성에서 인덱스가 생성된 경우(복합 인덱스) 인덱스를 편집한 후에 속성을 삭제할 수 있습니다.  
  
-   사용자 지정 인덱스에 포함된 속성 유형은 변경될 수 없습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|인덱스 만들기|[인덱스 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|인덱스 편집 및 삭제|[인덱스 편집 및 삭제&#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  

