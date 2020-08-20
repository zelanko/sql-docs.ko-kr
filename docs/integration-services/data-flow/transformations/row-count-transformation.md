---
description: 행 개수 변환
title: 행 개수 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a538c99d7f10e7bde271ed0ea622e05b4944a22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477625"
---
# <a name="row-count-transformation"></a>행 개수 변환

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  행 개수 변환은 행이 데이터 흐름을 통과할 때 행 수를 세어 최종 개수를 변수에 저장합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지는 행 개수를 사용하여 스크립트, 식 및 속성 식에 사용된 변수를 업데이트할 수 있습니다. (예를 들어 행 개수가 저장되는 변수는 행 개수가 포함되도록 전자 메일 메시지의 메시지 텍스트를 업데이트할 수 있습니다.) 행 개수 변환에 사용되는 변수는 이미 존재해야 하며 행 개수 변환이 포함된 데이터 흐름이 속해 있는 데이터 흐름 태스크의 범위 내에 있어야 합니다.  
  
 변환에서는 마지막 행이 변환을 통과한 후에만 변수에 행 개수 값을 저장합니다. 따라서 변수 값은 행 개수 변환이 포함된 데이터 흐름에서 업데이트된 값을 사용할 수 있도록 적시에 업데이트되지 않습니다. 업데이트된 변수는 별도의 데이터 흐름에서 사용할 수 있습니다.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-row-count-transformation"></a>행 개수 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 변수](../../../integration-services/integration-services-ssis-variables.md)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
