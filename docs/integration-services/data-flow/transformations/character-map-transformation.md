---
title: 문자표 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 88aa12fe6a02cce0788eab3ffafeb49769a9991f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112747"
---
# <a name="character-map-transformation"></a>문자표 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  문자표 변환은 소문자에서 대문자로의 변환과 같은 문자열 함수를 문자 데이터에 적용합니다. 이 변환은 문자열 데이터 형식의 열 데이터에서만 실행됩니다.  
  
 문자표 변환은 사용 중인 열 데이터를 변환하거나 열을 변환 출력에 추가하고 변환된 데이터를 새 열에 배치할 수 있습니다. 다양한 매핑 작업 집합을 동일한 입력 열에 적용하고 결과를 다른 열에 배치할 수 있습니다. 예를 들어 동일한 열을 대문자와 소문자로 변환하고 결과를 두 개의 서로 다른 열에 배치할 수 있습니다.  
  
 매핑으로 인해 데이터가 잘리는 경우도 있습니다. 예를 들어 싱글바이트 문자를 멀티바이트 표현 문자로 매핑하면 데이터가 잘릴 수 있습니다. 문자표 변환에는 잘린 데이터를 별도의 출력으로 보내는 데 사용할 수 있는 오류 출력이 있습니다. 자세한 내용은 [데이터 오류 처리](../../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="mapping-operations"></a>매핑 작업  
 다음 표에서는 문자표 변환이 지원하는 매핑 작업을 설명합니다.  
  
|연산|설명|  
|---------------|-----------------|  
|바이트 반전|바이트 순서를 반대로 바꿉니다.|  
|전자|반자 문자를 전자 문자에 매핑합니다.|  
|반자|전자 문자를 반자 문자에 매핑합니다.|  
|히라가나|가타카나 문자를 히라가나 문자에 매핑합니다.|  
|가타카나|히라가나 문자를 가타카나 문자에 매핑합니다.|  
|대/소문자 구분 기능|시스템 규칙 대신 대/소문자 구분 기능을 적용합니다. 대/소문자 구분 기능은 터키어 및 다른 로캘의 유니코드 단순 대/소문자 구분 매핑을 위해 Win32 API에서 제공하는 기능입니다.|  
|소문자|문자를 소문자로 변환합니다.|  
|중국어(간체)|중국어 번체 문자를 중국어 간체 문자에 매핑합니다.|  
|중국어(번체)|중국어 간체 문자를 중국어 번체 문자에 매핑합니다.|  
|대문자|문자를 대문자로 변환합니다.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>상호 배타적인 매핑 작업  
 한 변환에서 둘 이상의 작업을 수행할 수 있습니다. 그러나 일부 매핑 작업은 함께 사용할 수 없습니다. 다음 표에서는 동일한 열에 여러 개의 작업을 사용할 때 적용되는 제한을 나열합니다. 작업 A 열과 작업 B 열의 작업은 함께 사용할 수 없습니다.  
  
|작업 A|작업 B|  
|-----------------|-----------------|  
|소문자|대문자|  
|히라가나|가타카나|  
|반자|전자|  
|중국어(번체)|중국어(간체)|  
|소문자|히라가나, 가타카나, 반자, 전자|  
|대문자|히라가나, 가타카나, 반자, 전자|  
  
## <a name="configuration-of-the-character-map-transformation"></a>문자표 변환 구성  
 다음과 같은 방법으로 문자표 변환을 구성할 수 있습니다.  
  
-   변환할 열을 지정합니다.  
  
-   각 열에 적용할 작업을 지정합니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>문자표 변환 편집기
  **문자표 변환 편집기** 대화 상자를 사용하여 열 데이터에 적용할 문자열 함수를 선택하고 매핑이 내부 변경인지, 아니면 새 열로 추가되었는지를 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 확인란을 사용하여 문자열 함수로 변환할 열을 선택할 수 있습니다. 아래 테이블에 선택 내용이 나타납니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. 사용 가능한 입력 열 목록을 사용하여 선택 내용을 변경 또는 제거할 수도 있습니다.  
  
 **대상**  
 문자열 작업 결과를 기존 열을 사용하여 내부에 저장할지, 아니면 수정된 데이터를 새 열로 저장할지를 지정합니다.  
  
|값|설명|  
|-----------|-----------------|  
|새 열|새 열에 데이터를 저장합니다. **출력 별칭**의 열 이름을 할당합니다.|  
|내부 변경|수정된 데이터를 기존 열에 저장합니다.|  
  
 **연산**  
 열 데이터에 적용할 문자열 함수를 목록에서 선택합니다.  
  
|값|설명|  
|-----------|-----------------|  
|소문자|소문자로 변환합니다.|  
|대문자|대문자로 변환합니다.|  
|바이트 반전|바이트 순서를 반대로 바꿔 변환합니다.|  
|히라가나|일본어 가타카나 문자를 히라가나로 변환합니다.|  
|가타카나|일본어 히라가나 문자를 가타카나로 변환합니다.|  
|반자|전자 문자를 반자로 변환합니다.|  
|전자|반자 문자를 전자로 변환합니다.|  
|대/소문자 구분 기능|시스템 규칙 대신 대/소문자 구분 규칙(터키어 및 다른 로캘의 유니코드 단순 대/소문자 구분 매핑)을 적용합니다.|  
|중국어(간체)|중국어 번체 문자를 간체로 변환합니다.|  
|중국어(번체)|중국어 간체 문자를 번체로 변환합니다.|  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 **Copy of** 뒤에 입력 열 이름이 오는 형식이지만 설명이 포함된 고유 이름을 선택할 수 있습니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 이 변환에 대한 오류 처리 옵션을 지정할 수 있습니다.  
  
  
