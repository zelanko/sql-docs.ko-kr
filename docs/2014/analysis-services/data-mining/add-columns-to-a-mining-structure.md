---
title: 마이닝 구조에 열 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85a713bb9da24a67ebe8fdd097535c5a9d5ac98e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086233"
---
# <a name="add-columns-to-a-mining-structure"></a>마이닝 구조에 열 추가
  데이터 마이닝 마법사에서 마이닝 구조를 정의한 후 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 데이터 마이닝 디자이너를 사용하여 마이닝 구조에 열을 추가할 수 있습니다. 마이닝 구조 정의에 사용된 데이터 원본 뷰에 있는 열을 모두 추가할 수 있습니다.  
  
> [!NOTE]  
>  마이닝 구조에 열의 여러 복사본을 추가할 수 있지만, 원본과 파생 열 간에 잘못된 상관 관계를 방지하려면 동일한 모델 내에서 두 개 이상의 열 인스턴스를 사용하지 마십시오.  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>마이닝 구조에 열을 추가하려면  
  
1.  데이터 마이닝 디자이너에서 **마이닝 구조** 탭을 선택합니다.  
  
2.  마이닝 구조를 마우스 오른쪽 단추로 클릭하고 **열 추가**를 선택합니다.  
  
     
  **열 선택** 대화 상자가 열립니다.  
  
3.  
  **원본 테이블**에서 열이 있는 데이터 원본 뷰의 테이블을 선택합니다.  
  
4.  
  **원본 열**에서 마이닝 구조에 추가할 열을 선택합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  이미 있는 열을 추가하면 이름에 "1"이 붙은 복사본이 구조에 포함됩니다. 마이닝 구조 열의 **이름** 속성에 새 이름을 입력하여 복사된 열의 이름을 보다 설명적인 이름으로 변경할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조 태스크 및 방법](mining-structure-tasks-and-how-tos.md)  
  
  
