---
title: Excel (SSAS 테이블 형식)에서 분석 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8090c75108f7a384019030082699917fca915b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067684"
---
# <a name="analyze-in-excel-ssas-tabular"></a>Excel에서 분석(SSAS 테이블 형식)
  테이블 형식 모델 작성자는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 Excel에서 분석 기능을 사용하여 개발 중 신속하게 모델 프로젝트를 분석할 수 있습니다. Excel에서 분석 기능은 Microsoft Excel을 열고 모델 작업 영역 데이터베이스에 데이터 원본을 연결한 후 자동으로 워크시트에 피벗 테이블을 추가합니다. 피벗 테이블 필드 목록에 작업 영역 데이터베이스 개체(테이블, 열 및 측정값)가 필드로 포함됩니다. 그런 다음 유효 사용자 또는 역할 및 큐브 뷰의 컨텍스트 내에서 개체 및 데이터를 조회할 수 있습니다.  
  
 이 항목에서는 Microsoft Excel, 피벗 테이블 및 피벗 차트를 잘 알고 있다고 가정합니다. Excel 사용법에 대한 자세한 내용은 Excel 도움말을 참조하십시오.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_benefits)  
  
-   [관련 작업](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> 이점  
 모델 작성자는 Excel에서 분석 기능을 사용하여 일반적인 데이터 분석 애플리케이션인 Microsoft Excel으로 모델 프로젝트의 효율성을 테스트할 수 있습니다. Excel에서 분석 기능을 사용하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 실행하는 컴퓨터에 Microsoft Office 2003 이상이 설치되어 있어야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]와 동일한 컴퓨터에 Office가 설치되어 있지 않으면 다른 컴퓨터의 Excel을 사용하여 데이터 원본으로 작업 영역 데이터베이스에 연결할 수 있습니다. 그런 다음 워크시트에 피벗 테이블을 수동으로 추가할 수 있습니다.  
  
 Excel에서 분석 기능은 Excel을 실행하여 새 Excel 통합 문서(.xls)를 만듭니다. 통합 문서에 모델 작업 영역 데이터베이스에 대한 데이터 연결이 생성됩니다. 워크시트에 빈 피벗 테이블이 추가되고 피벗 테이블 필드 목록에 모델 개체 메타데이터가 채워집니다. 그런 다음 피벗 테이블에 보기 가능한 데이터 및 슬라이서를 추가할 수 있습니다.  
  
 Excel에서 분석 기능을 사용할 때는 기본적으로 현재 로그온한 사용자 계정이 유효 사용자가 됩니다. 이 계정은 주로 모델 개체 또는 데이터를 보는 데 제한이 없는 관리자이지만, 다른 유효 사용자 이름 또는 역할을 지정할 수도 있습니다. 이를 통해 Excel에서 특정 사용자 또는 역할 컨텍스트에 따라 모델 프로젝트를 검색할 수 있습니다. 유효 사용자 지정 시 다음과 같은 옵션이 있습니다.  
  
 **현재 Windows 사용자**  
 현재 로그온한 사용자 계정을 사용합니다.  
  
 **기타 Windows 사용자**  
 현재 로그온한 사용자가 아닌 다른 Windows 사용자 이름을 지정합니다. 다른 Windows 사용자를 사용할 때 암호는 필요 없습니다. Excel에서 유효 사용자 이름의 컨텍스트 내에서 개체 및 데이터에 대한 조회만 가능하며, 모델 개체 또는 데이터를 변경할 수 없습니다.  
  
 **역할**  
 역할은 개체 메타데이터 및 데이터에 대한 사용자 권한을 정의하는 데 사용됩니다. 역할은 일반적으로 특정 Windows 사용자 또는 Windows 사용자 그룹에 대해 정의됩니다. 일부 역할은 DAX 수식에서 정의하는 추가 행 수준 필터를 포함할 수 있습니다. Excel에서 분석 기능을 사용할 때 선택 사항으로 사용할 역할을 지정할 수 있습니다. 역할에 정의된 권한 및 필터에 따라 조회할 수 있는 개체 메타데이터 및 데이터가 제한됩니다. 자세한 내용은 [역할 만들기 및 관리&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)를 참조하세요.  
  
 유효 사용자 또는 역할 외에 큐브 뷰를 지정할 수 있습니다. 큐브 뷰를 사용하는 모델의 작성자는 모델 개체 및 데이터의 특정 비즈니스 시나리오 보기를 정의할 수 있습니다. 기본 설정은 큐브 뷰를 사용하지 않는 것입니다. Excel에서 분석 기능에서 큐브 뷰를 사용하려면 먼저 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 큐브 뷰 대화 상자를 사용하여 큐브 뷰가 정의되어 있어야 합니다. 큐브 뷰가 지정되면 피벗 테이블 필드 목록에 큐브 뷰에서 선택된 개체만 포함됩니다. 자세한 내용은 [큐브 뷰 만들기 및 관리&#40;SSAS 테이블 형식&#41;](perspectives-ssas-tabular.md)를 참조하세요.  
  
##  <a name="bkmk_rt"></a> 관련 태스크  
  
|**항목**|**설명**|  
|---------------|---------------------|  
|[Excel에서 테이블 형식 모델 분석&#40;SSAS 테이블 형식&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)|이 항목에서는 모델 디자이너에서 Excel에서 분석 기능을 사용하여 Excel을 열고, 모델 작업 영역 데이터베이스에 데이터 원본을 연결하고, 워크시트에 피벗 테이블을 추가하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Excel에서 테이블 형식 모델 분석&#40;SSAS 테이블 형식&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [역할&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)   
 [큐브 뷰&#40;SSAS 테이블 형식&#41;](perspectives-ssas-tabular.md)  
  
  
