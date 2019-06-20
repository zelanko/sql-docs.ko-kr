---
title: 플랫 파일 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6338c7a306f163f786f2c1e7d44ae4dbc66504ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902478"
---
# <a name="flat-file-source"></a>플랫 파일 원본
  플랫 파일 원본은 텍스트 파일에서 데이터를 읽습니다. 텍스트 파일은 구분 기호로 분리됨, 고정 폭 또는 혼합 형식 중 하나일 수 있습니다.  
  
-   구분 기호로 분리된 형식은 열 및 행 구분 기호를 사용하여 열과 행을 정의합니다.  
  
-   고정 폭 형식은 너비를 사용하여 열과 행을 정의합니다. 이 형식에는 최대 너비까지 필드를 패딩하는 문자도 포함됩니다.  
  
-   왼쪽 정렬 형식은 너비를 사용하여 모든 열을 정의하지만 마지막 열은 행 구분 기호로 분리됩니다.  
  
 다음과 같은 방법으로 플랫 파일 원본을 구성할 수 있습니다.  
  
-   플랫 파일 원본이 데이터를 추출할 텍스트 파일 이름이 포함된 열을 변환 출력에 추가합니다.  
  
-   플랫 파일 원본이 길이가 0인 열의 문자열을 Null 값으로 해석할지를 지정합니다.  
  
    > [!NOTE]  
    >  플랫 파일 원본이 사용하는 플랫 파일 연결 관리자에서 구분 기호로 분리된 형식을 사용하여 길이가 0인 문자열을 Null로 해석하도록 구성해야 합니다. 연결 관리자가 고정 폭 또는 왼쪽 정렬 형식을 사용하는 경우 공백으로 구성된 데이터를 Null 값으로 해석할 수 없습니다.  
  
 플랫 파일 원본 출력의 출력 열에는 FastParse 속성이 포함됩니다. FastParse는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 더 빠르지만 로캘을 구분하지 않는 빠른 구문 분석 루틴을 사용할지 또는 로캘을 구분하는 표준 구문 분석 루틴을 사용할지를 나타냅니다. 자세한 내용은 [Fast Parse](../fast-parse.md) 및 [Standard Parse](../standard-parse.md)를 참조하세요.  
  
 또한 출력 열에는 UseBinaryFormat 속성이 포함되어 있습니다. 이 속성을 사용하여 압축된 10진수 형식이 있는 데이터와 같은 이진 데이터에 대한 지원을 파일에서 구현할 수 있습니다. 기본적으로 UseBinaryFormat은 설정 `false`합니다. 이진 형식을 사용 하려는 경우로 UseBinaryFormat `true` 출력 열에는 데이터 형식 `DT_BYTES`합니다. 이렇게 설정할 경우 플랫 파일 원본은 데이터 변환을 건너뛰고 데이터를 있는 그대로 출력 열에 전달합니다. 그런 다음 파생 열 또는 데이터 변환과 같은 변환을 사용하여 `DT_BYTES` 데이터를 다른 데이터 형식에 캐스팅하거나 스크립트 변환에서 사용자 지정 스크립트를 작성하여 데이터를 해석할 수 있습니다. 또한 사용자 지정 데이터 흐름 구성 요소를 작성하여 데이터를 해석할 수 있습니다. 데이터 형식에 대 한 자세한 내용은 캐스팅할 수에 대 한 `DT_BYTES` 참조 하세요 [Cast &#40;식&#41;](../expressions/cast-ssis-expression.md)합니다.  
  
 이 원본은 플랫 파일 연결 관리자를 사용하여 텍스트 파일에 액세스합니다. 플랫 파일 연결 관리자의 속성을 설정하여 파일과 해당 파일의 각 열에 대한 정보를 제공하고 플랫 파일에서 텍스트 파일의 데이터를 처리하는 방법을 지정할 수 있습니다. 예를 들어 파일의 열과 행을 구분하는 문자와 각 열의 데이터 형식 및 길이를 지정할 수 있습니다. 자세한 내용은 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)을 참조하세요.  
  
 이 원본에는 출력 한 개와 오류 출력 한 개가 있습니다.  
  
## <a name="configuration-of-the-flat-file-source"></a>플랫 파일 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **플랫 파일 원본 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [플랫 파일 원본 편집기&#40;연결 관리자 페이지&#41;](../flat-file-source-editor-connection-manager-page.md)  
  
-   [플랫 파일 원본 편집기&#40;열 페이지&#41;](../flat-file-source-editor-columns-page.md)  
  
-   [플랫 파일 원본 편집기&#40;오류 출력 페이지&#41;](../flat-file-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../common-properties.md)  
  
-   [플랫 파일 사용자 지정 속성](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 데이터 흐름 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [플랫 파일 대상](flat-file-destination.md)   
 [데이터 흐름](data-flow.md)  
  
  
