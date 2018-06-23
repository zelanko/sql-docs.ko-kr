---
title: 마이닝 구조에서 열 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 85906ae2b1388b7937f5420ba04144426475ffc1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183723"
---
# <a name="remove-columns-from-a-mining-structure"></a>마이닝 구조에서 열 제거
  마이닝 구조를 만든 후 데이터 마이닝 디자이너를 사용하여 해당 구조에서 열을 제거할 수 있습니다. 마이닝 구조 열을 제거하는 이유는 다음과 같을 수 있습니다.  
  
-   마이닝 구조에 한 열의 여러 복사본이 포함되어 있으며 모델에 중복 데이터를 사용하지 않으려고 합니다.  
  
-   데이터를 보호해야 하지만 드릴스루를 사용하도록 설정되었습니다.  
  
-   데이터가 모델링에 사용되지 않으며 데이터를 처리해서는 안 됩니다.  
  
 마이닝 구조에서 열을 삭제하면 데이터 원본 뷰 또는 외부 데이터에서는 열이 변경되지 않고 메타데이터만 삭제됩니다. 그러나 마이닝 구조에서 사용되는 열을 변경하면 해당 구조 및 해당 구조를 기반으로 하는 모델을 모두 다시 처리해야 합니다.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>마이닝 구조에서 열을 제거하려면  
  
1.  데이터 마이닝 디자이너에서 **마이닝 구조** 탭을 선택합니다.  
  
2.  마이닝 구조 트리를 확장하여 모든 열을 표시합니다.  
  
3.  삭제할 열을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
4.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 구조 태스크 및 방법](mining-structure-tasks-and-how-tos.md)  
  
  