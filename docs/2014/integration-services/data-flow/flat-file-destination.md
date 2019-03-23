---
title: 플랫 파일 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30f8f566dc04726076dd9eb7c4d91b56f687218d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390231"
---
# <a name="flat-file-destination"></a>플랫 파일 대상
  플랫 파일 대상은 데이터를 텍스트 파일에 기록합니다. 텍스트 파일은 구분 기호로 분리된 형식, 고정 폭 형식, 행 구분 기호가 있는 고정 폭 형식 또는 왼쪽 정렬 형식일 수 있습니다.  
  
 다음과 같은 방법으로 플랫 파일 대상을 구성할 수 있습니다.  
  
-   데이터를 쓰기 전에 삽입할 텍스트 블록을 파일에 입력합니다. 텍스트는 열 제목과 같은 정보를 제공할 수 있습니다.  
  
-   같은 이름의 대상 파일에 데이터를 덮어쓸지 여부를 지정합니다.  
  
 이 대상은 플랫 파일 연결 관리자를 사용하여 텍스트 파일에 액세스합니다. 플랫 파일 대상에서 사용되는 플랫 파일 연결 관리자에 속성을 설정하여 플랫 파일 대상에서 텍스트 파일을 기록하고 형식을 지정하는 방식을 지정할 수 있습니다. 플랫 파일 연결 관리자를 구성할 때 파일 및 파일의 각 열에 대한 정보를 지정합니다. 예를 들어 파일의 열과 행을 구분하는 문자와 각 열의 데이터 형식 및 길이를 지정할 수 있습니다. 자세한 내용은 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)을 참조하세요.  
  
 플랫 파일 대상에는 Header 사용자 지정 속성이 포함됩니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../expressions/use-property-expressions-in-packages.md) 및 [플랫 파일 사용자 지정 속성](flat-file-custom-properties.md)을 참조하세요.  
  
 이 대상은 하나의 출력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-flat-file-destination"></a>플랫 파일 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **플랫 파일 원본 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [플랫 파일 대상 편집기&#40;연결 관리자 페이지&#41;](../flat-file-destination-editor-connection-manager-page.md)  
  
-   [플랫 파일 대상 편집기&#40;매핑 페이지&#41;](../flat-file-destination-editor-mappings-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../common-properties.md)  
  
-   [플랫 파일 사용자 지정 속성](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 데이터 흐름 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [플랫 파일 원본](flat-file-source.md)   
 [데이터 흐름](data-flow.md)  
  
  
