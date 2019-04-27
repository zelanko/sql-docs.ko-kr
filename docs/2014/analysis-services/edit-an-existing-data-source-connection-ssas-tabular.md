---
title: 기존 데이터 원본 연결 (SSAS 테이블 형식)를 편집 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.selexistconn.f1
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a177971e13a100044ccc40de44b93dbf6816478
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731572"
---
# <a name="edit-an-existing-data-source-connection-ssas-tabular"></a>기존 데이터 원본 연결 편집(SSAS 테이블 형식)
  이 항목에서는 테이블 형식 모델에서 기존 데이터 원본 연결의 속성을 편집하는 방법에 대해 설명합니다.  
  
 외부 데이터 원본에 대한 연결을 만든 후 나중에 다음과 같은 방법으로 연결을 수정할 수 있습니다.  
  
-   원본으로 사용된 파일, 피드 또는 데이터베이스, 해당 속성 또는 기타 공급자별 연결 옵션을 비롯한 연결 정보를 변경할 수 있습니다.  
  
-   테이블 및 열 매핑을 변경하고 더 이상 사용되지 않는 열에 대한 참조를 제거할 수 있습니다.  
  
-   외부 데이터 원본에서 가져오는 테이블, 뷰 또는 열을 변경할 수 있습니다.  
  
## <a name="modify-a-connection"></a>연결 수정  
 이 절차에서는 데이터베이스 데이터 원본 연결을 수정하는 방법을 설명합니다. 데이터 원본으로 작업하는 데 사용할 수 있는 일부 옵션은 데이터 원본의 유형에 따라 다르지만 그러한 차이를 쉽게 식별할 수 있습니다.  
  
#### <a name="to-change-the-external-data-source-used-by-a-current-connection"></a>현재 연결에 사용되는 외부 데이터 원본을 변경하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 **모델** 메뉴를 클릭한 다음 **기존 연결**을 클릭합니다.  
  
2.  수정하려는 데이터 원본 연결을 선택한 다음 **편집**을 클릭합니다.  
  
3.  **연결 편집** 대화 상자에서 **찾아보기** 를 클릭하여 유형은 같지만 이름이나 위치는 같지 않은 다른 데이터베이스를 찾습니다.  
  
     데이터베이스 파일을 변경하면 테이블을 저장하고 새로 고쳐야 새 데이터를 볼 수 있다는 메시지가 나타납니다.  
  
4.  **저장**을 클릭한 다음 **닫기**를 클릭합니다.  
  
5.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델**을 클릭하고 **처리**를 클릭한 다음 **모두 처리**를 클릭합니다.  
  
     새 데이터 원본을 사용하여 테이블이 다시 처리되지만 원래 선택된 데이터는 그대로 포함됩니다.  
  
    > [!NOTE]  
    >  새 데이터 원본에 원래 데이터 원본에는 없는 추가 테이블이 있는 경우 변경한 연결을 다시 열고 해당 테이블을 추가해야 합니다.  
  
## <a name="edit-table-and-column-mappings-bindings"></a>테이블 및 열 매핑(바인딩) 편집  
 이 절차에서는 데이터 원본을 변경한 후 매핑을 편집하는 방법에 대해 설명합니다.  
  
#### <a name="to-edit-column-mappings-when-a-data-source-changes"></a>데이터 원본을 변경할 때 열 매핑을 편집하려면  
  
1.  모델 디자이너에서 테이블을 선택합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **테이블 속성**을 클릭합니다.  
  
     선택한 테이블의 이름이 **테이블 이름** 상자에 표시됩니다. **원본 이름** 상자에는 외부 데이터 원본에 있는 테이블의 이름이 표시됩니다. 원본과 모델에서 열 이름이 서로 다를 경우 **원본** 또는 **모델**옵션을 선택하여 두 열 이름을 전환할 수 있습니다.  
  
3.  데이터 원본으로 사용되는 테이블을 변경하려면 **원본 이름**에서 현재 테이블이 아닌 다른 테이블을 선택합니다.  
  
4.  필요한 경우 열 매핑을 변경합니다.  
  
    1.  원본에는 있지만 모델에는 없는 열을 추가하려면 열 이름 옆의 확인란을 선택합니다.  
  
         다음에 모델을 새로 고칠 때 실제 데이터가 통합 문서에 로드됩니다.  
  
    2.  모델의 일부 열을 현재 데이터 원본에서 더 이상 사용할 수 없는 경우 잘못된 열을 보여 주는 메시지가 알림 영역에 나타납니다. 이 경우 별도의 작업을 수행할 필요가 없습니다.  
  
5.  **저장** 을 클릭하여 변경 내용을 모델에 적용합니다.  
  
     현재 테이블 속성 집합을 저장하면 테이블을 처리해야 한다는 메시지가 나타날 수 있습니다. **처리** 를 클릭하여 업데이트된 데이터를 모델에 로드합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 처리&#40;SSAS 테이블 형식&#41;](process-data-ssas-tabular.md)   
 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
