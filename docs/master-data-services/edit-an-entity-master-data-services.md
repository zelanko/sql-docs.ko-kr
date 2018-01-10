---
title: "엔터티 편집(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
caps.latest.revision: "8"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1db0dc3057958a282cd98c0ea72685354229fe6a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="edit-an-entity-master-data-services"></a>엔터티 편집(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 엔터티를 편집할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-edit-an-entity"></a>엔터티를 편집하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 변경할 엔터티의 행을 선택하고 **편집**을 클릭합니다.  
  
4.  **이름** 상자에 엔터티의 업데이트된 이름을 입력합니다.  
  
5.  **설명** 필드에 엔터티의 업데이트된 설명을 입력합니다.  
  
6.  **준비 테이블 이름** 대화 상자에서 준비 테이블의 업데이트된 이름을 입력합니다.  
  
7.  **트랜잭션 로그 유형** 필드의 드롭다운 목록에서 업데이트된 트랜잭션 로그 유형을 선택합니다.  
  
     자세한 내용은 [엔터티 트랜잭션 로그 유형 변경&#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)을 참조하세요.  
  
8.  **자동으로 코드 값 만들기** 확인란을 선택하거나 선택을 취소합니다.  
  
     자세한 내용은 [코드 자동 생성&#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)을 참조하세요.  
  
9. **데이터 압축 사용** 확인란을 선택하거나 선택을 취소합니다. 행 압축 기능은 기본적으로 설정됩니다.  
  
     자세한 내용은 [Data Compression](../relational-databases/data-compression/data-compression.md)를 참조하세요.  
  
## <a name="status"></a>상태  
 표의 상태 열에는 엔터티에 대한 작업의 상태가 표시됩니다. **엔터티 저장**을 클릭하면 엔터티가 업데이트되고 있음을 나타내는 다음 이미지가 표시됩니다.  
  
 ![업데이트 상태 아이콘](../master-data-services/media/mds-statusicon-updating.png "업데이트 상태 아이콘")  
  
 엔터티를 만들거나 편집할 때 오류가 발생하면 다음 이미지가 표시됩니다.  
  
 ![오류 상태 아이콘](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘")  
  
 엔터티가 정상 상태이면 다음 이미지가 표시됩니다.  
  
 ![정상 상태 아이콘](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘")  
  
## <a name="see-also"></a>참고 항목  
 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [엔터티 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [엔터티&#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
