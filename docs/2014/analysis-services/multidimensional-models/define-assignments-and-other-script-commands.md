---
title: 할당 및 기타 스크립트 명령 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e95dff588932bc7885d2501e3d24cc643ae10272
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241164"
---
# <a name="define-assignments-and-other-script-commands"></a>할당 및 기타 스크립트 명령 정의
  큐브 디자이너의 **계산** 탭에서 도구 모음의 **새 스크립트 명령** 아이콘을 클릭하여 빈 스크립트를 만듭니다. 새 스크립트를 만들면 처음에 계산 탭의 **스크립트 구성 도우미** 창에 빈 제목과 함께 해당 스크립트가 표시됩니다. 계산 식 창에 입력한 문자는 **스크립트 구성 도우미**의 항목 이름으로 표시됩니다. 따라서 첫 줄에 설명이 포함된 이름을 입력하여 **스크립트 구성 도우미** 창에서 해당 스크립트를 보다 쉽게 식별할 수 있습니다. 자세한 내용은 [Microsoft SQL Server 2005의 MDX 스크립팅 소개(Introduction to MDX Scripting in Microsoft SQL Server 2005)](https://go.microsoft.com/fwlink/?LinkId=81892)를 참조하십시오. MDX 쿼리 및 계산과 관련 된 성능 문제에 대 한 자세한 내용은 "효율적인 MDX 작성" 섹션을 참조 합니다 [SQL Server 2005 Analysis Services 성능 가이드](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)합니다.  
  
> [!IMPORTANT]  
>  처음에 큐브 디자이너의 **계산** 탭으로 전환하면 **스크립트 구성 도우미** 창에 CALCULATE 명령이 포함된 단일 스크립트가 있습니다. CALCULATE 명령은 큐브에 있는 셀의 집계를 제어하며 큐브 집계 방법을 수동으로 지정하려는 경우에만 편집해야 합니다.  
  
 계산 식 창을 사용하여 MDX(Multidimensional Expressions) 구문으로 식을 작성할 수 있습니다. 식을 작성하는 동안 **계산 도구** 창에서 계산 식 창으로 큐브 구성 요소, 함수 및 템플릿을 끌거나 복사할 수 있습니다. 그러면 계산 식 창에서 항목을 놓거나 붙여넣은 위치에 해당 항목의 스크립트가 추가됩니다. 인수와 구분 기호(« 및 »)를 적절한 값으로 바꿉니다.  
  
> [!IMPORTANT]  
>  계산 식 창을 사용하여 여러 문을 포함하는 식을 작성할 때는 MDX 스크립트의 마지막 줄을 제외한 모든 줄이 세미콜론(;)으로 끝나야 합니다. 계산은 단일 MDX 스크립트로 연결되며 각 스크립트에는 세미콜론이 추가되어 MDX 스크립트가 올바르게 컴파일되도록 합니다. 계산 식 창에서 스크립트의 마지막 줄에 세미콜론을 추가하면 큐브가 올바르게 생성되어 배포되지만 해당 큐브에 대해 쿼리를 실행할 수 없게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 계산](calculations-in-multidimensional-models.md)  
  
  
