---
title: "열 가져오기 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 13d509e0a064b7f8e831e41825496e745d88f831
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="import-column-transformation"></a>열 가져오기 변환
  열 가져오기 변환은 파일에서 데이터를 읽어 데이터 흐름의 열에 추가합니다. 이 변환을 사용하면 패키지가 별도의 파일에 저장된 텍스트와 이미지를 데이터 흐름에 추가할 수 있습니다. 예를 들어 제품 정보를 저장하는 테이블에 데이터를 로드하는 데이터 흐름은 파일에서 각 제품에 대한 고객 평가를 가져와서 데이터 흐름에 추가하는 열 가져오기 변환을 포함할 수 있습니다.  
  
 다음과 같은 방법으로 열 가져오기 변환을 구성할 수 있습니다.  
  
-   변환에서 데이터를 추가할 열을 지정합니다.  
  
-   변환에 BOM(바이트 순서 표시)이 필요한지를 지정합니다.  
  
    > [!NOTE]  
    >  BOM은 데이터가 DT_NTEXT 데이터 형식인 경우에만 필요합니다.  
  
 변환 입력의 열에는 데이터가 저장된 파일 이름이 포함됩니다. 데이터 집합의 각 행에서 서로 다른 파일을 지정할 수 있습니다. 열 가져오기 변환은 행을 처리할 때 파일 이름을 읽고 파일 시스템에서 해당 파일을 연 다음 파일 내용을 출력 열에 로드합니다. 출력 열의 데이터 형식은 DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="configuration-of-the-import-column-transformation"></a>열 가져오기 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [열 내보내기 변환](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

