---
description: 열 복사 변환
title: 열 복사 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 129cbbbc4c119a865f55567edc93900466013e39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477753"
---
# <a name="copy-column-transformation"></a>열 복사 변환

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  열 복사 변환은 입력 열을 복사하고 새 열을 변환 출력에 추가하여 새 열을 만듭니다. 데이터 흐름의 뒷부분에서 열 복사본에 다른 변환을 적용할 수 있습니다. 예를 들어 열 복사 변환을 사용하여 열 복사본을 만든 다음 문자표 변환을 사용하여 복사한 데이터를 대문자로 변환하거나 집계 변환을 사용하여 새 열에 집계를 적용할 수 있습니다.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>열 복사 변환 구성  
 복사할 입력 열을 지정하여 열 복사 변환을 구성합니다. 특정 열의 여러 복사본이나 여러 열의 복사본을 단일 작업으로 만들 수 있습니다.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="copy-column-transformation-editor"></a>열 복사 변환 편집기
  **열 복사 변환 편집기** 대화 상자를 사용하여 복사할 열을 선택하고 새 출력 열의 이름을 할당할 수 있습니다.  
  
> [!NOTE]  
>  사용자가 모든 원본 데이터를 대상에 간단하게 복사할 경우 열 복사 변환을 사용할 필요가 없을 수 있습니다. 일부 시나리오에서는 데이터 변환이 필요하지 않을 때 원본을 대상에 직접 연결할 수 있습니다. 이러한 상황에서는 SQL Server 가져오기 및 내보내기 마법사를 사용하여 패키지를 만드는 것이 좋습니다. 필요한 경우 나중에 패키지를 향상시키고 다시 구성할 수 있습니다. 자세한 내용은 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 확인란을 사용하여 복사할 열을 선택합니다. 선택한 항목은 아래의 입력 열에 추가됩니다.  
  
 **입력 열**  
 사용 가능한 입력 열 목록에서 복사할 열을 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열** 테이블의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 새 출력 열의 별칭을 입력합니다. 기본값은 **사본 -** 뒤에 입력 열의 이름이 오는 형식이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
