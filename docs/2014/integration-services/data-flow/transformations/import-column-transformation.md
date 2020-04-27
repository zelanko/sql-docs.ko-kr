---
title: 열 가져오기 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13deb9b423ce20fd77e0853cba9d0f205905ca44
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770425"
---
# <a name="import-column-transformation"></a>열 가져오기 변환
  열 가져오기 변환은 파일에서 데이터를 읽어 데이터 흐름의 열에 추가합니다. 이 변환을 사용하면 패키지가 별도의 파일에 저장된 텍스트와 이미지를 데이터 흐름에 추가할 수 있습니다. 예를 들어 제품 정보를 저장하는 테이블에 데이터를 로드하는 데이터 흐름은 파일에서 각 제품에 대한 고객 평가를 가져와서 데이터 흐름에 추가하는 열 가져오기 변환을 포함할 수 있습니다.  
  
 다음과 같은 방법으로 열 가져오기 변환을 구성할 수 있습니다.  
  
-   변환에서 데이터를 추가할 열을 지정합니다.  
  
-   변환에 BOM(바이트 순서 표시)이 필요한지를 지정합니다.  
  
    > [!NOTE]  
    >  BOM은 데이터가 DT_NTEXT 데이터 형식인 경우에만 필요합니다.  
  
 변환 입력의 열에는 데이터가 저장된 파일 이름이 포함됩니다. 데이터 세트의 각 행에서 서로 다른 파일을 지정할 수 있습니다. 열 가져오기 변환은 행을 처리할 때 파일 이름을 읽고 파일 시스템에서 해당 파일을 연 다음 파일 내용을 출력 열에 로드합니다. 출력 열의 데이터 형식은 DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 자세한 내용은 [Integration Services Data Types](../integration-services-data-types.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="configuration-of-the-import-column-transformation"></a>열 가져오기 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../../common-properties.md)  
  
-   [변환 사용자 지정 속성](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [열 내보내기 변환](export-column-transformation.md)   
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
