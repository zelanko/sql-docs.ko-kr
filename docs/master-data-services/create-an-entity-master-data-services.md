---
title: 엔터티 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 686c3f487207a430136feac2588e4b4b2dda9b1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65476999"
---
# <a name="create-an-entity-master-data-services"></a>엔터티 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 멤버와 해당 특성을 포함할 엔터티를 만듭니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   모델이 있어야 합니다. 자세한 내용은 [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-an-entity"></a>엔터티를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 엔터티를 만들 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 **추가**를 클릭합니다.  
  
4.  **이름** 상자에 엔터티의 이름을 입력합니다.  
  
5.  필요에 따라 **설명** 필드에 엔터티 설명을 입력합니다.  
  
6.  필요에 따라 **준비 테이블 이름** 상자에 준비 테이블의 이름을 입력합니다.  
  
     이 필드에 이름을 입력하지 않으면 엔터티 이름이 사용됩니다.  
  
    > [!TIP]  
    >  모델 이름을 준비 테이블의 일부로 사용합니다(예: *Modelname_Entityname*). 그러면 데이터베이스에서 테이블을 더 쉽게 찾을 수 있습니다. 준비 테이블에 대한 자세한 내용은 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요.
    > [!TIP]
    > 준비 테이블에 대해 기본 이름을 사용하는 경우 동일한 이름의 엔터티가 다른 모델에 존재하면 MDS는 준비 테이블 이름에 식별자(예: _1, _2)를 자동으로 추가합니다.
  
7.  **트랜잭션 로그 유형** 필드의 드롭다운 목록에서 트랜잭션 로그 유형을 선택합니다.  
  
     자세한 내용은 [엔터티 트랜잭션 로그 유형 변경&#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)을 참조하세요.  
  
8.  (선택 사항) **코드 값 자동으로 만들기** 확인란을 선택합니다. 자세한 내용은 [코드 자동 생성&#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)을 참조하세요.  
  
9. (선택 사항) **데이터 압축 사용** 확인란을 선택합니다. 행 압축 기능은 기본적으로 설정됩니다. 자세한 내용은 [Data Compression](../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
10. **저장**을 클릭합니다.  
  
## <a name="grid-columns"></a>표 형태의 열  
 생성되는 각 엔터티에 대해 열이 13개 포함된 행이 표에 추가됩니다. 이러한 열은 다음과 같습니다.  
  
|이름|Description|  
|----------|-----------------|  
|상태|엔터티 상태입니다. **저장** 을 클릭하면 엔터티가 업데이트되고 있음을 나타내는 다음 이미지가 표시됩니다.<br /><br /> ![업데이트 상태 아이콘](../master-data-services/media/mds-statusicon-updating.png "업데이트 상태 아이콘")<br /><br /> 엔터티를 만들거나 편집할 때 오류가 발생하면 다음 이미지가 표시됩니다.<br /><br /> ![오류 상태 아이콘](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘")<br /><br /> 엔터티가 정상 상태이면 다음 이미지가 표시됩니다.<br /><br /> ![정상 상태 아이콘](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘")|  
|이름|엔터티 이름입니다.|  
|Description|엔터티 설명입니다.|  
|준비 테이블|데이터 저장에 사용되는 테이블의 접두사 이름입니다.|  
|트랜잭션 로그 유형|엔터티의 트랜잭션 로그 유형입니다.|  
|코드 자동 생성|코드 자동 생성을 사용할지 여부를 지정합니다.|  
|Data Compression|엔터티에 대해 데이터 압축을 사용할지 여부를 지정합니다.|  
|동기화 대상|엔터티가 동기화 관계의 대상인지 여부를 지정합니다.|  
|계층 사용|명시적 계층에 엔터티를 사용할지 여부를 지정합니다. 엔터티에 대해 명시적 계층을 하나 이상 만들면 이 열에는 예가 표시됩니다.|  
|만든 사람|엔터티를 만든 사용자의 사용자 이름입니다.|  
|만든 날짜|엔터티를 만든 날짜와 시간입니다.|  
|업데이트한 사람|엔터티를 마지막으로 업데이트한 사용자의 사용자 이름입니다.|  
|업데이트한 날짜|엔터티를 마지막으로 업데이트한 날짜 및 시간입니다.|  
  
## <a name="next-steps"></a>다음 단계  
  
-   [텍스트 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [파일 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [엔터티&#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [엔터티 편집&#40;Master Data Services&#41;](../master-data-services/edit-an-entity-master-data-services.md)   
 [엔터티 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)  
  
  
