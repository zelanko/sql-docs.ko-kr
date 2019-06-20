---
title: 데이터 흐름 속성 식을 사용 하 여 설정할 수 있는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70a956834108c21dd7b17bb9f3e04db38f29bfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059938"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>식을 사용하여 설정할 수 있는 데이터 흐름 속성
  데이터 흐름 태스크 컨테이너에서 사용할 수 있는 속성 식을 사용하여 데이터 흐름 개체의 특정 속성 값을 지정할 수 있습니다.  
  
 속성 식을 사용하는 방법은 [패키지에서 속성 식 사용](expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 속성 식을 사용하여 배포된 패키지의 각 인스턴스 구성을 사용자 지정할 수 있습니다. 또한 속성 식을 사용하여 **dtexec** 명령 프롬프트 유틸리티로 **/set** 옵션을 사용해 패키지의 런타임 제약 조건을 지정할 수도 있습니다. 예를 들어 정렬 변환에 사용된 `MaximumThreads` 또는 유사 항목 그룹화 및 유사 항목 조회 변환의 `MaxMemoryUsage`를 제약할 수 있습니다. 제약 받지 않을 경우 이러한 변환은 메모리에 대량의 데이터를 캐시할 수 있습니다.  
  
 이 항목에 나열된 데이터 흐름 개체의 속성 중 하나에 대한 속성 식을 지정하려면 디자이너의 **제어 흐름** 화면에서 데이터 흐름 태스크를 선택하거나 개별 구성 요소나 경로를 선택하지 않고 디자이너의 **데이터 흐름** 탭을 선택하여 데이터 흐름 태스크에 대한 **속성** 창을 표시합니다. **식** 속성을 선택하고 줄임표(...)를 클릭하여 **속성 식 편집기** 대화 상자를 표시합니다. **속성** 목록을 드롭다운하여 속성을 선택한 다음 **식** 입력란에 식을 입력하거나 줄임표(...)를 클릭하여 **식 작성기** 대화 상자를 표시합니다.  
  
 **속성** 목록에는 디자이너의 **데이터 흐름** 화면에 이미 배치한 이러한 데이터 흐름 개체에 사용할 수 있는 속성만 표시됩니다. 따라서 **속성** 목록을 사용하여 속성 식을 지원하는 데이터 흐름 개체의 가능한 모든 속성을 확인할 수는 없습니다. 예를 들어 ADO NET 원본을 디자이너 화면에 배치 했으면 합니다 **속성** 목록에 대 한 항목이 `[ADO NET Source].[SqlCommand]` 속성입니다. 목록에는 데이터 흐름 태스크 자체의 수많은 속성도 표시됩니다.  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>속성 식을 지원하는 데이터 흐름 개체의 속성  
 다음 목록의 속성 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
### <a name="data-flow-sources"></a>데이터 흐름 원본  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|ADO.NET 원본|TableOrViewName 속성<br /><br /> SQLCommand 속성|  
|XML 원본|XMLData 속성<br /><br /> XMLSchemaDefinition 속성|  
  
### <a name="data-flow-transformations"></a>데이터 흐름 변환  
 이러한 사용자 지정 속성에 대한 자세한 내용은 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)을 참조하십시오.  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|조건부 분할 변환|FriendlyExpression 속성|  
|파생 열 변환|FriendlyExpression 속성|  
|유사 항목 그룹화 변환|MaxMemoryUsage 속성|  
|유사 항목 조회 변환|MaxMemoryUsage 속성|  
|조회 변환|SQLCommand 속성<br /><br /> SqlCommandParam 속성|  
|OLE DB 명령 변환|SQLCommand 속성|  
|비율 샘플링 변환|SamplingValue 속성|  
|피벗 변환|PivotKeyValue 속성|  
|행 샘플링 변환|SamplingValue 속성|  
|정렬 변환|MaximumThreads 속성|  
|피벗 해제 변환|PivotKeyValue 속성|  
  
### <a name="data-flow-destinations"></a>데이터 흐름 대상  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|ADO.NET 대상|TableOrViewName 속성<br /><br /> BatchSize 속성<br /><br /> CommandTimeout 속성|  
|플랫 파일 대상|Header 속성|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 대상|TableName 속성|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 대상|BulkInsertTableName 속성<br /><br /> BulkInsertFirstRow 속성<br /><br /> BulkInsertLastRow 속성<br /><br /> BulkInsertOrder 속성<br /><br /> Timeout 속성|  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>관련 내용  
 pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)  
  
## <a name="see-also"></a>관련 항목  
 [패키지에서 속성 식 사용](expressions/use-property-expressions-in-packages.md)   
 [공용 속성](../../2014/integration-services/common-properties.md)   
 [변환 사용자 지정 속성](data-flow/transformations/transformation-custom-properties.md)   
 [경로 속성](../../2014/integration-services/path-properties.md)  
  
  
