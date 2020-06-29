---
title: 열 내보내기 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2914c6a23a326f4d312c2784eaad2b84fdad0b0e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430650"
---
# <a name="export-column-transformation"></a>열 내보내기 변환
  열 내보내기 변환은 데이터 흐름에서 데이터를 읽어 파일에 삽입합니다. 예를 들어 데이터 흐름에 각 제품 사진과 같은 제품 정보가 포함되어 있으면 열 내보내기 변환을 사용하여 이미지를 파일에 저장할 수 있습니다.  
  
## <a name="append-and-truncate-options"></a>추가 및 잘림 옵션  
 다음 표에서는 추가 및 잘림 옵션 설정이 결과에 미치는 영향을 설명합니다.  
  
|추가|Truncate|파일 존재 여부|결과|  
|------------|--------------|-----------------|-------------|  
|False|False|예|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|True|False|예|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|False|True|예|이 변환은 새 파일을 만들고 해당 파일에 데이터를 씁니다.|  
|True|True|예|이 변환은 디자인 타임 유효성 검사에 실패합니다. 두 속성을 모두 `true`로 설정하면 안 됩니다.|  
|False|False|yes|런타임 오류가 발생합니다. 이 변환은 파일은 있지만 해당 파일에 쓸 수 없습니다.|  
|False|True|yes|이 변환은 파일을 삭제하고 다시 만든 후 해당 파일에 데이터를 씁니다.|  
|True|False|yes|이 변환은 파일을 열고 해당 파일의 끝에 데이터를 씁니다.|  
|True|True|yes|이 변환은 디자인 타임 유효성 검사에 실패합니다. 두 속성을 모두 `true`로 설정하면 안 됩니다.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>열 내보내기 변환 구성  
 다음과 같은 방법으로 열 내보내기 변환을 구성할 수 있습니다.  
  
-   데이터를 쓸 파일 경로가 포함된 열과 데이터 열을 지정합니다.  
  
-   데이터 삽입 작업에서 기존 파일을 추가하거나 잘라낼지를 지정합니다.  
  
-   파일에 BOM(바이트 순서 표시)을 쓸지를 지정합니다.  
  
    > [!NOTE]  
    >  기존 파일에 데이터를 추가하지 않으며 데이터 형식이 DT_NTEXT인 경우에만 BOM이 기록됩니다.  
  
 이 변환은 입력 열의 쌍을 사용합니다. 그 중 하나에는 파일 이름이 있고 다른 하나에는 데이터가 있습니다. 데이터 집합의 각 행에서 서로 다른 파일을 지정할 수 있습니다. 변환이 행을 처리하면 지정한 파일에 데이터가 삽입됩니다. 런타임 시 파일이 존재하지 않을 경우 이 변환은 새로 파일을 만든 후 데이터를 해당 파일에 씁니다. 기록될 데이터 형식은 DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 자세한 내용은 [Integration Services Data Types](../integration-services-data-types.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **열 내보내기 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [열 내보내기 변환 편집기&#40;열 페이지&#41;](../../export-column-transformation-editor-columns-page.md)를 참조하세요.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
