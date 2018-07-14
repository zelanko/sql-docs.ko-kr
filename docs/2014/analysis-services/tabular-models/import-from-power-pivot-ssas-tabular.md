---
title: PowerPivot에서 가져오기 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f6480cf0b577a0faa48691a85248efb77a84531
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245743"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>PowerPivot에서 가져오기(SSAS 테이블 형식)
  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 PowerPivot에서 가져오기 프로젝트 템플릿을 사용하여 PowerPivot 통합 문서에서 메타데이터와 데이터를 가져와서 새로운 테이블 형식 모델 프로젝트를 만드는 방법에 대해 설명합니다.  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>Excel 파일용 Powerpivot에서 새 테이블 형식 모델 만들기  
 PowerPivot 통합 문서에서 가져와서 새로운 테이블 형식 모델 프로젝트를 만드는 경우 통합 문서의 구조를 정의하는 메타데이터를 사용하여 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 테이블 형식 모델 프로젝트의 구조를 만들고 정의합니다. 테이블, 열, 측정값 및 관계와 같은 개체는 그대로 유지되며 PowerPivot 통합 문서에 표시되는 것과 똑같이 테이블 형식 모델 프로젝트에 표시됩니다. .xlsx 통합 문서 파일은 변경되지 않습니다.  
  
> [!NOTE]  
>  테이블 형식 모델은 연결된 테이블을 지원하지 않습니다. 연결된 테이블이 포함된 PowerPivot 통합 문서에서 가져오는 경우 연결된 테이블 데이터는 복사/붙여 넣은 데이터로 처리되며 Model.bim 파일에 저장됩니다. 복사하여 붙여넣은 테이블의 속성을 볼 때 **원본 데이터** 속성은 비활성화되고 **테이블** 메뉴의 **테이블 속성** 대화 상자도 비활성화됩니다.  
>   
>  모델에 포함된 데이터에 추가할 수 있는 행은 최대 10,000개로 제한됩니다. PowerPivot에서 모델을 가져오는 경우 “데이터가 잘렸습니다. 붙여 넣은 테이블은 행을 10000개 이상 포함할 수 없습니다.” 오류가 표시됩니다. 포함된 데이터를 다른 데이터 원본(예를 들어 SQL Server의 테이블)으로 이동하여 PowerPivot 모델을 수정한 다음 다시 가져와야 합니다.  
  
 작업 영역 데이터베이스가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 와 동일한 컴퓨터(로컬)의 Analysis Services 인스턴스에 있는지, 아니면 원격 Analysis Services 인스턴스에 있는지에 따라 특별히 고려해야 할 사항이 있습니다.  
  
 작업 영역 데이터베이스가 Analysis Services의 로컬 인스턴스에 있는 경우 PowerPivot 통합 문서에서 메타데이터와 데이터를 모두 가져올 수 있습니다. 메타데이터는 통합 문서에서 복사되고 테이블 형식 모델 프로젝트를 만드는 데 사용됩니다. 그런 다음 데이터가 통합 문서에서 복사되고 프로젝트의 작업 영역 데이터베이스에 저장됩니다(복사/붙여넣은 데이터는 제외되며 이러한 데이터는 Model.bim 파일에 저장됨).  
  
 작업 영역 데이터베이스가 원격 Analysis Services 인스턴스에 있는 경우 PowerPivot for Excel 통합 문서에서 데이터를 가져올 수 없습니다. 통합 문서 메타데이터를 여전히 가져올 수 있지만 이렇게 하면 스크립트가 원격 Analysis Services 인스턴스에서 실행됩니다. 신뢰할 수 있는 PowerPivot 통합 문서에서만 메타데이터를 가져와야 합니다. 데이터 원본 연결에 정의된 원본에서 데이터를 가져와야 합니다. PowerPivot 통합 문서의 복사/붙여 넣은 테이블 데이터와 연결된 테이블 데이터를 복사하여 테이블 형식 모델 프로젝트에 붙여 넣어야 합니다.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>PowerPivot for Excel 파일에서 새 테이블 형식 모델 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.  
  
2.  에 **새 프로젝트** 대화 상자의 **설치 된 템플릿**, 클릭 **Business Intelligence**를 클릭 하 고 **PowerPivot에서가져오기**.  
  
3.  **이름**에 프로젝트의 이름을 입력하고 위치 및 솔루션 이름을 지정한 다음 **확인**을 클릭합니다.  
  
4.  **열기** 대화 상자에서 가져올 모델 메타데이터 및 데이터가 포함된 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 파일을 선택한 다음 **열기**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [작업 영역 데이터베이스 &#40;&AMP;#40;SSAS 테이블 형식&#41;](workspace-database-ssas-tabular.md)   
 [데이터 복사 및 붙여넣기 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../copy-and-paste-data-ssas-tabular.md)  
  
  
