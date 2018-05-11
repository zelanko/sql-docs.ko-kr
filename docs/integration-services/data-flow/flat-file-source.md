---
title: 플랫 파일 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1accfd1edea180ea20ae09f1ef8fbf8d0c54ad40
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
 플랫 파일 원본 출력의 출력 열에는 FastParse 속성이 포함됩니다. FastParse는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 더 빠르지만 로캘을 구분하지 않는 빠른 구문 분석 루틴을 사용할지 또는 로캘을 구분하는 표준 구문 분석 루틴을 사용할지를 나타냅니다. 자세한 내용은 [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 및 [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)를 참조하세요.  
  
 또한 출력 열에는 UseBinaryFormat 속성이 포함되어 있습니다. 이 속성을 사용하여 압축된 10진수 형식이 있는 데이터와 같은 이진 데이터에 대한 지원을 파일에서 구현할 수 있습니다. 기본적으로 UseBinaryFormat은 **false**로 설정됩니다. 이진 형식을 사용하려면 UseBinaryFormat을 **true** 로 설정하고 출력 열의 데이터 형식을 **DT_BYTES**로 설정합니다. 이렇게 설정할 경우 플랫 파일 원본은 데이터 변환을 건너뛰고 데이터를 있는 그대로 출력 열에 전달합니다. 그런 다음 파생 열 또는 데이터 변환과 같은 변환을 사용하여 **DT_BYTES** 데이터를 다른 데이터 형식으로 캐스팅하거나 스크립트 변환에서 사용자 지정 스크립트를 작성하여 데이터를 해석할 수 있습니다. 또한 사용자 지정 데이터 흐름 구성 요소를 작성하여 데이터를 해석할 수 있습니다. **DT_BYTES**를 캐스팅할 수 있는 데이터 형식에 대한 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
 이 원본은 플랫 파일 연결 관리자를 사용하여 텍스트 파일에 액세스합니다. 플랫 파일 연결 관리자의 속성을 설정하여 파일과 해당 파일의 각 열에 대한 정보를 제공하고 플랫 파일에서 텍스트 파일의 데이터를 처리하는 방법을 지정할 수 있습니다. 예를 들어 파일의 열과 행을 구분하는 문자와 각 열의 데이터 형식 및 길이를 지정할 수 있습니다. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을 참조하세요.  
  
 이 원본에는 출력 한 개와 오류 출력 한 개가 있습니다.  
  
## <a name="configuration-of-the-flat-file-source"></a>플랫 파일 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [플랫 파일 사용자 지정 속성](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 데이터 흐름 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>플랫 파일 원본 편집기(연결 관리자 페이지)
  **플랫 파일 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 플랫 파일 원본이 사용할 연결 관리자를 선택할 수 있습니다. 플랫 파일 원본은 구분 기호로 분리된 텍스트 파일, 고정 폭 텍스트 파일 또는 혼합 형식의 텍스트 파일에서 데이터를 읽을 수 있습니다.  
  
 플랫 파일 원본은 다음과 같은 연결 관리자 유형 중 하나를 사용할 수 있습니다.  
  
-   원본이 단일 플랫 파일인 경우 플랫 파일 연결 관리자. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을(를) 참조하세요.  
  
-   원본이 다중 플랫 파일이고 데이터 흐름 태스크가 For 루프 컨테이너와 같은 루프 컨테이너 내부에 있는 경우 다중 플랫 파일 연결 관리자. 각 컨테이너 루프에서 플랫 파일 원본은 다중 플랫 파일 연결 관리자가 제공하는 다음 파일 이름에서 데이터를 로드합니다. 자세한 내용은 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)을 참조하세요.  
  
### <a name="options"></a>변수  
 **Flat file connection manager**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **새로 만들기**  
 **플랫 파일 연결 관리자 편집기** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지**  
 데이터를 추출할 때 Null 값을 유지할지 여부를 지정합니다. 이 속성의 기본값은 **false**입니다. 이 값이 f**alse**이면 플랫 파일 원본이 원본 데이터의 Null 값을 각 열에 적합한 기본값으로 바꿉니다. 예를 들어 문자열 열의 경우 빈 문자열로 바꾸고 숫자 열의 경우 0으로 바꿉니다.  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="flat-file-source-editor-columns-page"></a>플랫 파일 원본 편집기(열 페이지)
  **플랫 파일 원본 편집기** 대화 상자의 **열** 노드를 사용하여 출력 열을 외부(원본) 열에 매핑할 수 있습니다.  
  
> [!NOTE]  
>  플랫 파일 원본의 **FileNameColumnName** 속성과 해당 출력 열의 **FastParse** 속성은 **플랫 파일 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md)의 플랫 파일 원본 섹션을 참조하십시오.  
  
### <a name="options"></a>변수  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 표시합니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다.  
  
 **외부 열**  
 태스크에서 읽는 순서대로 외부(원본) 열을 표시합니다. 이 순서는 먼저 테이블에서 선택된 열을 지운 다음 목록에서 다른 순서로 외부 열을 선택하여 변경할 수 있습니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
## <a name="flat-file-source-editor-error-output-page"></a>플랫 파일 원본 편집기(오류 출력 페이지)
  **플랫 파일 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택하고 오류 출력 열의 속성을 설정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **플랫 파일 원본 편집기** 대화 상자의 **연결 관리자**페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **잘림**  
 잘림이 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 오류에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [플랫 파일 대상](../../integration-services/data-flow/flat-file-destination.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
