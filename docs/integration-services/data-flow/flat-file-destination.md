---
title: 플랫 파일 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c649a4d31129d3719a3a648547b2139c767b6e61
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="flat-file-destination"></a>플랫 파일 대상
  플랫 파일 대상은 데이터를 텍스트 파일에 기록합니다. 텍스트 파일은 구분 기호로 분리된 형식, 고정 폭 형식, 행 구분 기호가 있는 고정 폭 형식 또는 왼쪽 정렬 형식일 수 있습니다.  
  
 다음과 같은 방법으로 플랫 파일 대상을 구성할 수 있습니다.  
  
-   데이터를 쓰기 전에 삽입할 텍스트 블록을 파일에 입력합니다. 텍스트는 열 제목과 같은 정보를 제공할 수 있습니다.  
  
-   같은 이름의 대상 파일에 데이터를 덮어쓸지 여부를 지정합니다.  
  
 이 대상은 플랫 파일 연결 관리자를 사용하여 텍스트 파일에 액세스합니다. 플랫 파일 대상에서 사용되는 플랫 파일 연결 관리자에 속성을 설정하여 플랫 파일 대상에서 텍스트 파일을 기록하고 형식을 지정하는 방식을 지정할 수 있습니다. 플랫 파일 연결 관리자를 구성할 때 파일 및 파일의 각 열에 대한 정보를 지정합니다. 예를 들어 파일의 열과 행을 구분하는 문자와 각 열의 데이터 형식 및 길이를 지정할 수 있습니다. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을 참조하세요.  
  
 플랫 파일 대상에는 Header 사용자 지정 속성이 포함됩니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [플랫 파일 사용자 지정 속성](../../integration-services/data-flow/flat-file-custom-properties.md)을 참조하세요.  
  
 이 대상은 하나의 출력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-flat-file-destination"></a>플랫 파일 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [플랫 파일 사용자 지정 속성](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 데이터 흐름 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>플랫 파일 대상 편집기(연결 관리자 페이지)
  **플랫 파일 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 사용할 플랫 파일 연결을 선택하고, 덮어쓸 것인지 아니면 기존 대상 파일에 추가할 것인지를 지정할 수 있습니다. 플랫 파일 대상에서는 텍스트 파일에 데이터를 기록합니다. 이 텍스트 파일은 구분 기호로 분리하거나 고정 폭, 구분 기호 있는 고정 폭 또는 왼쪽 정렬 중 하나를 사용할 수 있습니다.  
  
### <a name="options"></a>변수  
 **플랫 파일 연결 관리자**  
 목록 상자를 사용하여 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **플랫 파일 형식** 대화 상자와 **플랫 파일 연결 관리자 편집기** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **플랫 파일 형식** 대화 상자에는 표준 플랫 파일 형식인 구분 기호로 분리됨, 고정 폭 및 왼쪽 정렬 이외에도 **고정 폭, 행 구분 기호 사용**옵션이 표시됩니다. 이 옵션은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 더미 열을 데이터의 마지막 열로 추가할 때 사용하는 왼쪽 정렬 형식의 특별한 경우를 나타냅니다. 이 더미 열은 마지막 열이 고정 폭을 갖도록 합니다.  
  
 **고정 폭, 행 구분 기호 사용** 옵션은 **플랫 파일 연결 관리자 편집기**에서 사용할 수 없습니다. 필요한 경우 편집기에서 이 옵션을 에뮬레이트할 수는 있습니다. 이 옵션을 에뮬레이트하려면 **플랫 파일 연결 관리자 편집기** 대화 상자의 **일반**페이지에서 **형식**으로 **왼쪽 정렬**을 선택합니다. 그런 다음 편집기의 **고급** 페이지에서 새 더미 열을 데이터의 마지막 열로 추가합니다.  
  
 **파일의 데이터 덮어쓰기**  
 기존 파일을 덮어쓸지 아니면 기존 파일에 데이터를 추가할지 여부를 나타냅니다.  
  
 **머리글**  
 데이터를 쓰기 전에 삽입할 텍스트 블록을 입력합니다. 이 옵션을 사용하여 열 머리글 등의 추가 정보를 포함할 수 있습니다.  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="flat-file-destination-editor-mappings-page"></a>플랫 파일 대상 편집기(매핑 페이지)
  **플랫 파일 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 사용 가능한 입력 열을 대상 열에 매핑할 수 있습니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 사용 가능한 대상 열을 입력 열에 매핑할 수 있습니다.  
  
 **입력 열**  
 이 항목의 앞부분에서 선택한 입력 열을 표시합니다. **사용 가능한 입력 열**의 목록을 사용하여 매핑을 변경할 수 있습니다. 출력에서 열을 제외하려면 **\<무시>** 를 선택합니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [플랫 파일 원본](../../integration-services/data-flow/flat-file-source.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
