---
title: 열 내보내기 변환 | Microsoft Docs
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
- sql13.dts.designer.exportcolumntrans.f1
- sql13.dts.designer.fileextractortransformation.columns.f1
- sql13.dts.designer.fileextractortransformation.errorhandling.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e51d79c8d365bb1ba5b28feec4ab19ce445e234a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="export-column-transformation"></a>열 내보내기 변환
  열 내보내기 변환은 데이터 흐름에서 데이터를 읽어 파일에 삽입합니다. 예를 들어 데이터 흐름에 각 제품 사진과 같은 제품 정보가 포함되어 있으면 열 내보내기 변환을 사용하여 이미지를 파일에 저장할 수 있습니다.  
  
## <a name="append-and-truncate-options"></a>추가 및 잘림 옵션  
 다음 표에서는 추가 및 잘림 옵션 설정이 결과에 미치는 영향을 설명합니다.  
  
|추가|잘라내기|파일 존재 여부|결과|  
|------------|--------------|-----------------|-------------|  
|False|False|아니오|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|True|False|아니오|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|False|True|아니오|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|True|True|아니오|이 변환은 디자인 타임 유효성 검사에 실패합니다. 두 속성을 모두 **true**로 설정하면 안 됩니다.|  
|False|False|예|런타임 오류가 발생합니다. 이 변환은 파일은 있지만 해당 파일에 쓸 수 없습니다.|  
|False|True|예|이 변환은 파일을 삭제하고 다시 만든 후 해당 파일에 데이터를 씁니다.|  
|True|False|예|이 변환은 파일을 열고 해당 파일의 끝에 데이터를 씁니다.|  
|True|True|예|이 변환은 디자인 타임 유효성 검사에 실패합니다. 두 속성을 모두 **true**로 설정하면 안 됩니다.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>열 내보내기 변환 구성  
 다음과 같은 방법으로 열 내보내기 변환을 구성할 수 있습니다.  
  
-   데이터를 쓸 파일 경로가 포함된 열과 데이터 열을 지정합니다.  
  
-   데이터 삽입 작업에서 기존 파일을 추가하거나 잘라낼지를 지정합니다.  
  
-   파일에 BOM(바이트 순서 표시)을 쓸지를 지정합니다.  
  
    > [!NOTE]  
    >  기존 파일에 데이터를 추가하지 않으며 데이터 형식이 DT_NTEXT인 경우에만 BOM이 기록됩니다.  
  
 이 변환은 입력 열의 쌍을 사용합니다. 그 중 하나에는 파일 이름이 있고 다른 하나에는 데이터가 있습니다. 데이터 집합의 각 행에서 서로 다른 파일을 지정할 수 있습니다. 변환이 행을 처리하면 지정한 파일에 데이터가 삽입됩니다. 런타임 시 파일이 존재하지 않을 경우 이 변환은 새로 파일을 만든 후 데이터를 해당 파일에 씁니다. 기록될 데이터 형식은 DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="export-column-transformation-editor-columns-page"></a>열 내보내기 변환 편집기(열 페이지)
  **열 내보내기 변환 편집기** 대화 상자의 **열** 페이지를 사용하여 데이터 흐름에서 파일로 추출할 열을 지정할 수 있습니다. 열 내보내기 변환 시 데이터를 파일에 추가할 것인지, 아니면 기존 파일을 덮어쓸 것인지를 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **추출 열**  
 텍스트 또는 이미지 데이터를 포함하는 입력 열 목록에서 선택합니다. 모든 행에 **추출 열** 과 **파일 경로 열**에 대한 정의가 있어야 합니다.  
  
 **파일 경로 열**  
 파일 경로 및 파일 이름을 포함하는 입력 열 목록에서 선택합니다. 모든 행에 **추출 열** 과 **파일 경로 열**에 대한 정의가 있어야 합니다.  
  
 **추가 허용**  
 변환 시 데이터를 기존 파일에 추가할 것인지 여부를 지정합니다. 기본값은 **false**입니다.  
  
 **강제 자름**  
 변환 시 데이터를 쓰기 전에 기존 파일의 내용을 삭제할 것인지를 지정합니다. 기본값은 **false**입니다.  
  
 **BOM 쓰기**  
 BOM(바이트 순서 표시)을 파일에 쓸 것인지 여부를 지정합니다. 데이터 형식이 **DT_NTEXT** 또는 DT_WSTR이고 기존 데이터 파일에 추가되지 않는 경우에만 BOM을 씁니다.  
  
## <a name="export-column-transformation-editor-error-output-page"></a>열 내보내기 변환 편집기(오류 출력 페이지)
  **열 내보내기 변환 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 방법을 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **입/출력**  
 출력의 이름을 확인합니다. 이름을 클릭하여 열을 포함할 뷰를 확장할 수 있습니다.  
  
 **열**  
 **열 내보내기 변환 편집기** 대화 상자의 **열** 페이지에서 선택한 출력 열을 표시합니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **잘림**  
 잘림이 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 작업에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
  
