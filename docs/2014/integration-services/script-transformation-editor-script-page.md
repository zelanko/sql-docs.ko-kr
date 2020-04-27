---
title: 스크립트 변환 편집기 (스크립트 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script Transformation Editor
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1628acc984433b1def07c63387b1630c902885aa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056068"
---
# <a name="script-transformation-editor-script-page"></a>스크립트 변환 편집기(스크립트 페이지)
  **스크립트 변환 편집기** 대화 상자의 **스크립트** 탭을 사용하여 스크립트 및 관련 속성을 지정할 수 있습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [Script Component](data-flow/transformations/script-component.md) 및 [Configuring the Script Component in the Script Component Editor](extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하십시오. 스크립트 구성 요소 프로그래밍 방법은 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **속성**  
 스크립트 변환 속성을 보고 수정합니다. 표시된 속성 중 다수는 읽기 전용입니다. 다음 속성을 수정할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**설명**|스크립트 변환의 목적을 기준으로 스크립트 변환을 설명합니다.|  
|**LocaleID**|정렬과 날짜 및 시간 변환에 사용할 지역별 정보를 제공하는 로캘을 지정합니다.|  
|**이름**|구성 요소에 대한 설명이 포함된 이름을 입력합니다.|  
|**ValidateExternalMetadata**|스크립트 변환이 디자인 타임에서 외부 데이터 원본에 대해 열 메타데이터의 유효성을 검사할 것인지 여부를 나타냅니다. 값 `false`는 실행 시간까지 유효성 검사를 지연합니다.|  
|**ReadOnlyVariables**|스크립트 변환을 통해 읽기 전용으로 액세스할 변수 목록을 쉼표로 구분하여 입력합니다.<br /><br /> 참고: 변수 이름은 대/소문자를 구분합니다.|  
|**ReadWriteVariables**|스크립트 변환을 통해 읽기/쓰기로 액세스할 변수 목록을 쉼표로 구분하여 입력합니다.<br /><br /> 참고: 변수 이름은 대/소문자를 구분합니다.|  
|**ScriptLanguage**|스크립트 구성 요소에 사용될 스크립트 언어를 선택합니다.<br /><br /> 스크립트 구성 요소 및 스크립트 태스크에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [General Page](general-page-of-integration-services-designers-options.md)을 참조하세요.|  
|**UserComponentTypeName**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인프라를 지원하는 `Microsoft.SqlServer.TxScript` 어셈블리 및 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> 클래스를 지정합니다.|  
  
 **스크립트 편집**  
 VSTA [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (Tools for Applications)를 사용 하 여 스크립트를 만들거나 수정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [스크립트 구성 요소 유형 선택](../../2014/integration-services/select-script-component-type.md)   
 [스크립트 변환 편집기 &#40;입력 열 페이지&#41;](../../2014/integration-services/script-transformation-editor-input-columns-page.md)   
 [스크립트 변환 편집기 &#40;입력 및 출력 페이지&#41;](../../2014/integration-services/script-transformation-editor-inputs-and-outputs-page.md)   
 [스크립트 변환 편집기 &#40;연결 관리자 페이지&#41;](../../2014/integration-services/script-transformation-editor-connection-managers-page.md)   
 [추가 스크립트 구성 요소 예](extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  
