---
title: Excel에서 테이블 형식 모델 분석 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.chooseperspect.f1
ms.assetid: 47fa45fc-60ab-41a1-bde3-5781c8462889
author: minewiskan
ms.author: owend
ms.openlocfilehash: 36b28a97b920e5c43644451ebee1e0c50df019c2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939939"
---
# <a name="analyze-a-tabular-model-in-excel-ssas-tabular"></a>Excel에서 테이블 형식 모델 분석(SSAS 테이블 형식)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 Excel에서 분석 기능은 Microsoft Excel을 열고 모델 작업 영역 데이터베이스에 데이터 원본을 연결한 후 워크시트에 피벗 테이블을 추가합니다. 피벗 테이블 필드 목록에 모델 개체(테이블, 열, 측정값, 계층 및 KPI)가 필드로 포함됩니다.  
  
> [!NOTE]  
>  Excel에서 분석 기능을 사용하려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 실행하는 컴퓨터에 Microsoft Office 2003 이상 버전이 설치되어 있어야 합니다. 컴퓨터에 Office가 설치되어 있지 않을 경우 다른 컴퓨터의 Excel을 사용하여 데이터 원본으로 모델 작업 영역 데이터베이스에 연결할 수 있습니다. 그런 다음 워크시트에 피벗 테이블을 수동으로 추가할 수 있습니다. 피벗 테이블 필드 목록에 모델 개체(테이블, 열, 측정값 및 KPI)가 필드로 포함됩니다.  
  
## <a name="tasks"></a>작업  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>Excel에서 분석 기능을 사용하여 테이블 형식 모델 프로젝트를 분석하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **Excel에서 분석**을 클릭합니다.  
  
2.  **자격 증명 및 큐브 뷰 선택** 대화 상자에서 다음 자격 증명 옵션 중 하나를 선택하여 모델 작업 영역 데이터 원본에 연결합니다.  
  
    -   현재 사용자 계정을 사용하려면 **현재 Windows 사용자**를 선택합니다.  
  
    -   다른 사용자 계정을 사용하려면 **기타 Windows 사용자**를 선택합니다.  
  
         일반적으로 이 사용자 계정은 역할의 멤버입니다. 암호는 필요하지 않습니다. 이 계정은 작업 영역 데이터베이스에 대한 Excel 연결의 컨텍스트에서만 사용할 수 있습니다.  
  
    -   보안 역할을 사용하려면 **역할**을 선택한 다음 목록 상자에서 하나 이상의 역할을 선택합니다.  
  
         보안 역할은 역할 관리자를 사용하여 정의해야 합니다. 자세한 내용은 [역할 만들기 및 관리&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)를 참조하세요.  
  
3.  큐브 뷰를 사용하려면 **큐브 뷰** 목록 상자에서 큐브 뷰를 선택합니다.  
  
     기본값이 아닌 큐브 뷰는 큐브 뷰 대화 상자를 사용하여 정의해야 합니다. 자세한 내용은 [SSAS 테이블 형식&#41;&#40;큐브 뷰 만들기 및 관리 ](perspectives-ssas-tabular.md)를 참조 하세요.  
  
> [!NOTE]  
>  모델 디자이너에서 모델 프로젝트를 변경해도 Excel의 피벗 테이블 필드 목록에 자동으로 반영되지 않습니다. 피벗 테이블 필드 목록을 새로 고치려면 Excel의 **옵션** 리본에서 **새로 고침**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)  
  
  
