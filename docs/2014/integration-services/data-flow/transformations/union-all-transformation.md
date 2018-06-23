---
title: UNION ALL 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.unionalltrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 27547f95d50bd4552e766184f163dcd3b94a3bb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187241"
---
# <a name="union-all-transformation"></a>UNION ALL 변환
  UNION ALL 변환은 여러 개의 입력을 하나의 출력으로 결합합니다. 예를 들어 5개 플랫 파일 원본의 출력이 UNION ALL 변환의 입력이 되어 하나의 출력으로 결합될 수 있습니다.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 변환 입력은 하나씩 변환 출력에 추가되며 행이 다시 정렬되지 않습니다. 패키지에 정렬된 출력이 필요할 경우 UNION ALL 변환 대신 병합 변환을 사용해야 합니다.  
  
 UNION ALL 변환에 연결한 첫 번째 입력이 변환 출력을 만드는 데 사용됩니다. 변환에 연결한 이후 입력 열은 변환 출력 열에 매핑됩니다.  
  
 입력을 병합하려면 입력 열을 출력 열에 매핑합니다. 하나 이상의 입력 열을 각 출력 열에 매핑해야 합니다. 두 열을 매핑하려면 해당 열의 메타데이터가 일치해야 합니다. 예를 들어 매핑된 열의 데이터 형식이 같아야 합니다.  
  
 매핑된 열에 문자열 데이터가 포함되어 있고 출력 열의 길이가 입력 열보다 짧으면 입력 열을 포함할 수 있도록 출력 열의 길이가 자동으로 증가합니다. 출력 열에 매핑되지 않은 입력 열은 출력 열에서 Null 값으로 설정됩니다.  
  
 이 변환에는 여러 개의 입력과 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-union-all-transformation"></a>UNION ALL 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **UNION ALL 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Union All Transformation Editor](../../union-all-transformation-editor.md)를 참조하십시오.  
  
 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용은 [Common Properties](../../common-properties.md)을 참조하십시오.  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [UNION ALL 변환을 사용하여 데이터 병합](union-all-transformation.md)  
  
  