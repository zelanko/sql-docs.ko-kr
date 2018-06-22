---
title: 개체 바인딩 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.objectbinding.f1
helpviewer_keywords:
- Object Binding dialog box
ms.assetid: 2bb5ad7c-2962-4559-8c95-cf7148bd2e72
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13b0050733b21e99ac7395a26953338f4dbce176
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090260"
---
# <a name="object-binding-dialog-box"></a>개체 바인딩 대화 상자
  **의** 개체 바인딩 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체 속성과 데이터 원본 뷰의 테이블 또는 열 속성 간의 바인딩을 정의할 수 있습니다. **의** 속성 **창에서** 개체의 다음 속성 값에 대한 드롭다운 목록에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (새로 만들기) **를 선택하면** 개체 바인딩 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]대화 상자를 표시할 수 있습니다.  
  
-   NameColumn  
  
-   ValueColumn  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   UnaryOperatorColumn  
  
## <a name="options"></a>변수  
 **바인딩 유형**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에 사용할 바인딩을 선택합니다. 다음 바인딩 유형을 사용할 수 있습니다.  
  
 열 바인딩  
 개체를 데이터 원본 뷰의 기존 테이블 및 열에 바인딩합니다.  
  
 열 생성  
 데이터 원본 뷰에서 새 열이 정의된 다음 열 바인딩이 이 열과 연결됨을 나타냅니다.  
  
> [!NOTE]  
>  이 옵션을 선택하는 경우 **개체를 배포하기 전에** 스키마 생성 마법사 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 실행해야 합니다.  
  
 행 바인딩  
 개체를 팩트 테이블의 행에 바인딩합니다. 팩트 테이블에서 처리된 행 수를 기반으로 카운트 측정을 용이하게 하는 데 사용됩니다.  
  
 **원본 테이블**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체와 연결된 데이터 원본 뷰의 테이블 목록을 표시합니다.  
  
 **원본 열**  
 **원본 테이블**에서 선택한 테이블의 열 목록을 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  