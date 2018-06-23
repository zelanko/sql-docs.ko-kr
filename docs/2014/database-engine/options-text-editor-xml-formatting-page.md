---
title: 옵션 (텍스트 편집기-XML 서식 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5d77f7351d712f63e9cfc92c3ff03b131cb6d5d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080487"
---
# <a name="options-text-editor---xml---formatting-page"></a>옵션(텍스트 편집기 - XML - 서식 페이지)
  이 대화 상자를 사용하여 XML 편집기의 서식 설정을 지정할 수 있습니다. **옵션** 대화 상자는 **도구** 메뉴에서 액세스할 수 있습니다.  
  
> [!NOTE]  
>  이러한 설정은 **옵션** 대화 상자에서 **텍스트 편집기** 폴더,**XML** 폴더, **서식** 옵션을 차례로 선택할 때 사용할 수 있습니다.  
  
## <a name="attributes"></a>특성  
 **특성 수동 서식 유지**  
 특성 서식을 다시 설정하지 마십시오. 기본값입니다.  
  
> [!NOTE]  
>  특성이 여러 줄로 된 경우 편집기에서 상위 요소의 들여쓰기에 맞게 특성의 각 줄을 들여씁니다.  
  
 **별도 줄에 각 특성 정렬**  
 첫 번째 특성의 들여쓰기에 맞게 두 번째 및 이후의 특성을 세로로 정렬합니다. 다음 XML 텍스트는 특성 정렬 방법의 예입니다.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>자동 서식 다시 설정  
 **클립보드에서 붙여 넣을 합니다.**  
 클립보드에서 붙여 넣은 XML 텍스트 서식을 다시 설정합니다.  
  
 **끝 태그 완료 시**  
 끝 태그가 완료될 때 요소 서식을 다시 설정합니다.  
  
## <a name="mixed-content"></a>혼합된 콘텐츠  
 **기본값으로 혼합된 콘텐츠 서식 지정 합니다.**  
 `xml:space="preserve"` 범위에 콘텐츠가 있을 때를 제외하고 혼합된 콘텐츠 서식을 다시 설정하려고 합니다. 기본값입니다.  
  
 요소에 텍스트와 마크업이 혼합되어 있으면 콘텐츠가 혼합된 콘텐츠로 간주됩니다. 다음은 혼합된 콘텐츠가 있는 요소의 예입니다.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</dir >  
  
## <a name="see-also"></a>관련 항목  
 [XML 편집기&#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
  
  