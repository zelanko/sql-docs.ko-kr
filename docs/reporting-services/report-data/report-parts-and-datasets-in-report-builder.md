---
title: 보고서 작성기의 보고서 파트 및 데이터 세트 | Microsoft Docs
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a06344a119dfba635a07d0050a61f561065a2984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571192"
---
# <a name="report-parts-and-datasets-in-report-builder"></a>보고서 작성기의 보고서 파트 및 데이터 세트
  보고서 작성기에서 보고서에 데이터를 포함하는 가장 쉬운 방법은 보고서 파트 갤러리에서 보고서 파트를 추가하는 것입니다. 보고서 파트에는 파트가 종속되는 *종속 데이터 세트*라는 데이터 세트가 들어 있습니다. 종속 데이터 세트는 공유 데이터 원본을 기반으로 하며 포함된 데이터 세트 또는 공유 데이터 세트일 수 있습니다. [보고서 파트](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)에 대해 자세히 알아봅니다.  
  
 보고서에 데이터를 포함하는 또 다른 쉬운 방법은 공유 데이터 세트를 사용하는 것입니다. 자세한 내용은 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> 종속 데이터 세트가 포함된 보고서 파트를 보고서에 추가  
 보고서에 보고서 파트를 추가하면 해당 파트에 포함된 종속 데이터 세트도 보고서에 추가됩니다. 보고서 파트에는 기타 보고서 항목이 다수 들어 있는 사각형을 포함할 수 있으므로 보고서에 종속 데이터 세트가 여러 개 추가될 수 있습니다. 각 공유 데이터 세트는 독립 참조이므로 공유 데이터 세트가 종속되는 공유 데이터 원본은 보고서에 추가되지 않습니다. 각 포함된 데이터 세트 역시 자신이 종속되는 공유 데이터 원본이나 포함된 데이터 원본을 추가합니다.  
  
 포함된 데이터 원본의 자격 증명은 보고서 파트의 일부로 저장되지 않습니다. 포함된 데이터 원본을 보고서에 추가하는 경우에는 보고서를 실행할 때 자격 증명을 제공하라는 메시지가 표시됩니다. 이 메시지가 표시되지 않도록 하려면 공유 데이터 원본을 기반으로 하며 자격 증명이 저장되어 있는 보고서 파트를 사용하십시오.  
  
 보고서에 보고서 파트를 추가한 후에도 추가된 데이터 세트는 사용자가 만드는 공유 데이터 세트 또는 포함된 데이터 세트와 아무런 차이가 없습니다. 보고서 데이터 창에서 추가 데이터 세트를 확인할 수 있습니다. 포함된 데이터 세트는 해당하는 공유 데이터 원본 아래에, 공유 데이터 세트는 공유 데이터 세트 폴더 아래에 표시됩니다.  
  
##  <a name="Customizing"></a> 종속 데이터 세트 사용자 지정  
 보고서 파트를 보고서에 추가한 후에는 미리 보기를 통해 데이터 변경 여부를 결정할 수 있습니다. 변경 가능한 내용은 사용 중인 데이터 세트 유형에 따라 다릅니다.  
  
 포함된 데이터 세트의 데이터 및 데이터 옵션을 변경하려면 데이터 세트를 만들었을 때처럼 쿼리를 비롯한 데이터 세트 속성을 편집하면 됩니다.  
  
 공유 데이터 세트의 데이터 및 데이터 옵션을 변경하려면 보고서 서버에서 공유 데이터 세트 정의를 변경하면 됩니다. 단, 이 경우 해당하는 사용 권한이 있어야 합니다. 필터와 계산 필드를 추가하고 대/소문자 구분 등의 데이터 옵션을 변경하여 보고서에서 공유 데이터 세트 인스턴스를 사용자 지정할 수도 있습니다. 자세한 내용은 [포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
 공유 데이터 세트의 정의를 변경하는 방법 또는 보고서에서 공유 데이터 세트의 최신 데이터 변경 내용을 표시하는 방법에 대한 자세한 내용은 [공유 데이터 세트 또는 포함된 데이터 세트 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) 및 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Publishing"></a> 공유 데이터 세트로 종속 데이터 세트 게시  
 종속 데이터 세트가 포함된 보고서 항목을 게시할 때는 각 데이터 세트를 공유 데이터 세트 또는 포함된 데이터 세트(보고서 항목에 포함된 상태로 유지됨)로 게시할 수 있습니다.  
  
 공유 데이터 세트 옵션을 선택하면 데이터 세트가 공유 데이터 세트 정의로 보고서 서버에 저장됩니다. 보고서에서 해당 데이터 세트를 사용하는 모든 보고서 항목은 현재 보고서 서버에 있는 공유 데이터 세트를 가리키도록 업데이트됩니다. 그러면 다음과 같은 결과가 발생합니다.  
  
1.  게시 대화 상자에서 게시된 각 공유 데이터 세트가 게시 가능한 항목 목록에서 제거됩니다.  
  
2.  보고서 작성기를 끝내거나 새 보고서를 시작할 때 보고서를 저장하라는 메시지가 표시됩니다. 보고서를 저장하지 않는 경우 다음 번에 해당 보고서를 열어 보고서 항목을 게시할 때 같은 데이터 세트의 새 복사본이 게시될 수 있습니다. 공유 데이터 세트의 여러 복사본이 보고서 서버에 저장되지 않도록 하려면 보고서를 저장하는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  자신과 다른 사용자가 공유 데이터 세트의 데이터를 계속 정상적으로 사용하도록 하려면 보고서 항목 보안 관련 원칙을 이해해야 합니다. 자세한 내용은 [공유 데이터 세트 항목 보안 설정](../../reporting-services/security/secure-shared-dataset-items.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 디자인 뷰&#40;보고서 작성기&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [보안&#40;보고서 작성기&#41;](../../reporting-services/report-builder/security-report-builder.md)   
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
