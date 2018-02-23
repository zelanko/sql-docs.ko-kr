---
title: "SSMS를 사용 하 여 역할 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9472bef0e1971c3f8868902b5cd91189256e860d
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="manage-roles-by-using-ssms"></a>SSMS를 사용하여 역할 관리 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 배포된 테이블 형식 모델에 대한 역할을 생성, 편집 및 관리할 수 있습니다.  
  
 이 항목의 태스크:  
  
-   [새 역할을 만들려면](#bkmk_new_role)  
  
-   [역할 복사](#bkmk_copy_role)  
  
-   [역할 편집](#bkmk_edit_role)  
  
-   [역할을 삭제하려면](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 역할 관리자를 사용하여 정의한 역할로 테이블 형식 모델 프로젝트를 다시 배포하면 배포된 테이블 형식 모델에 정의된 역할을 덮어씁니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 모델 프로젝트가 열려 있는 동안 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 테이블 형식 모델 작업 영역 데이터베이스를 관리하면 Model.bim 파일이 손상될 수 있습니다. 테이블 형식 모델 작업 영역 데이터베이스에 대한 역할을 만들고 관리하는 경우 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 역할 관리자를 사용하십시오.  
  
###  <a name="bkmk_new_role"></a> 새 역할을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 역할을 만들 테이블 형식 model 데이터베이스를 확장하고 **역할**을 마우스 오른쪽 단추로 클릭한 다음 **새 역할**을 클릭합니다.  
  
2.  **역할 만들기** 대화 상자의 페이지 선택 창에서 **일반**을 클릭합니다.  
  
3.  일반 설정 창의 **이름** 필드에 역할의 이름을 입력합니다.  
  
     기본적으로 기본 역할의 이름은 새 역할을 만들 때마다 증분식으로 번호가 지정됩니다. 따라서 재무 관리자 또는 인적 자원 전문가와 같이 멤버 유형을 분명하게 식별하는 이름을 입력하는 것이 좋습니다.  
  
4.  **이 역할에 대한 데이터베이스 권한 설정**에서 다음 사용 권한 옵션 중 하나를 선택합니다.  
  
    |사용 권한|Description|  
    |----------------|-----------------|  
    |**모든 권한(관리자)**|멤버는 모델 스키마를 수정할 수 있으며 모든 데이터를 볼 수 있습니다.|  
    |**데이터베이스 처리**|멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다. 모델 스키마를 수정할 수 없으며 데이터를 볼 수 없습니다.|  
    |**읽기**|멤버는 행 필터를 기반으로 데이터를 볼 수 있지만 모델 스키마를 변경할 수 없습니다.|  
  
5.  **역할 만들기** 대화 상자의 페이지 선택 창에서 **멤버 자격**을 클릭합니다.  
  
6.  **멤버 자격 설정 창에서 추가**를 클릭한 다음 **사용자 또는 그룹 선택** 대화 상자에서 멤버로 추가할 Windows 사용자 또는 그룹을 추가합니다.  
  
7.  만들고 있는 역할에 읽기 권한이 있는 경우 DAX 수식을 사용하여 테이블에 대한 행 필터를 추가할 수 있습니다. 행 필터를 추가 하려면는 **역할 속성- \<rolename >** 대화 상자의 **페이지 선택**, 클릭 **행 필터**합니다.  
  
8.  행 필터 창에서 테이블을 클릭 한 다음는 **DAX 필터** 필드를 선택한 후는 **DAX 필터- \<tablename >** 필드에 DAX 수식을 입력 합니다.  
  
    > [!NOTE]  
    >  DAX 필터- \<tablename > 필드 자동 완성 쿼리 편집기를 포함 하지 않거나 함수 삽입 기능이 있습니다. DAX 수식을 작성할 때 자동 완성을 사용하려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 DAX 수식 편집기를 사용해야 합니다.  
  
9. **확인** 을 클릭하여 역할을 저장합니다.  
  
###  <a name="bkmk_copy_role"></a> 역할 복사  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 복사할 역할을 포함하는 테이블 형식 model 데이터베이스와 **역할**을 차례로 확장하고 역할을 마우스 오른쪽 단추로 클릭한 다음 **중복**을 클릭합니다.  
  
###  <a name="bkmk_edit_role"></a> 역할 편집  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 편집할 역할을 포함하는 테이블 형식 model 데이터베이스와 **역할**을 차례로 확장하고 역할을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
     에 **역할 속성** \<역할 이름 > 대화 상자는 추가/편집 행 필터 및 사용 권한 변경, 추가 또는 구성원을 제거할 수 있습니다.  
  
###  <a name="bkmk_deletet_role"></a> 역할을 삭제하려면  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 삭제할 역할을 포함하는 테이블 형식 model 데이터베이스와 **역할**을 차례로 확장하고 역할을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
