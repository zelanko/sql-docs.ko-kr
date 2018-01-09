---
title: "UPDATE MEMBER 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE_MEMBER
- UPDATE MEMBER
- MEMBER
- UPDATE
helpviewer_keywords:
- calculated members [MDX]
- UPDATE MEMBER statement
ms.assetid: 07ab708d-d165-4fb1-a9f9-fb8197ff0dab
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e126f34be1f1cecd1a793b71ff4b64069c1802c3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---update-member"></a>MDX 데이터 정의-UPDATE MEMBER
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  기존 계산 멤버를 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 멤버가 포함된 큐브의 이름을 지정하는 유효한 문자열입니다.  
  
 *Member_Name*  
 기존 멤버의 이름을 지정하는 유효한 문자열입니다.  
  
 *MDX_Expression*  
 멤버가 업데이트되는 유효한 MDX 식입니다.  
  
 *Property_Name*  
 계산 멤버 속성의 이름을 지정하는 유효한 문자열입니다.  
  
 *Property_Value*  
 계산 멤버의 속성 값을 지정하는 유효한 스칼라 식입니다.  
  
## <a name="remarks"></a>주의  
 UPDATE MEMBER 문은 다른 계산에 따라 이 멤버의 상대적 우선 순위는 보존하면서 기존 계산 멤버를 업데이트합니다. 따라서 UPDATE MEMBER 문을 사용하여 SOLVEORDER를 변경할 수 없습니다.  
  
 UPDATE MEMBER 문은 큐브의 MDX 스크립트에 지정할 수 없습니다.  
  
 현재 연결된 큐브가 아닌 다른 큐브를 지정하면 오류가 발생합니다. 따라서 큐브 이름에서 CURRENTCUBE를 사용하여 현재 큐브를 표시해야 합니다.  
  
 OLE DB에 의해 정의되는 멤버 속성에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="standard-properties"></a>표준 속성  
 각 멤버에는 기본 속성 집합이 있습니다. 다음 표에서는 이 기본 속성에 대해 설명합니다.  
  
|속성 식별자|의미|  
|-------------------------|-------------|  
|FORMAT_STRING|A [!INCLUDE[msCoName](../includes/msconame-md.md)] 클라이언트 응용 프로그램 셀 값을 표시 하는 데 사용할 수 있는 Office 스타일 서식 문자열입니다.|  
|VISIBLE|계산 멤버를 스키마 행 집합에서 볼 수 있는지 여부를 나타내는 값입니다.  계산 된 집합에 멤버를 추가할 수는 [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) 함수입니다. 0이 아닌 값은 계산 멤버를 볼 수 있음을 나타냅니다. 이 속성에 대 한 기본값은 *Visible*합니다.<br /><br /> 볼 수 없는 계산 멤버는 일반적으로 더 복잡한 계산 멤버에서 중간 단계로 사용됩니다. 이런 계산 멤버는 측정값과 같은 다른 종류의 멤버가 참조할 수도 있습니다.|  
|NON_EMPTY_BEHAVIOR|빈 셀을 확인할 때 계산 멤버의 동작을 결정하기 위해 MDX가 사용하는 측정값 또는 집합입니다.|  
|CAPTION|클라이언트 응용 프로그램이 멤버를 표시하기 위해 사용하는 캡션을 지정하는 문자열 값입니다.|  
|DISPLAY_FOLDER|클라이언트 응용 프로그램이 멤버를 표시하는 표시 폴더의 경로를 지정하는 문자열 값입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 정의 멤버에 대해 여러 표시 폴더를 제공하려면 세미콜론(;)을 사용하여 폴더를 구분하십시오.|  
|ASSOCIATED_MEASURE_GROUP|이 멤버를 연결할 측정값 그룹의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [DROP MEMBER 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [MEMBER 문 &#40; 만들기 Mdx&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
