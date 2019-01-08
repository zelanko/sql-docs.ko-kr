---
title: 문자표 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11aaa19aebce21cc8a0ba08038c1dc58f245ec2d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761825"
---
# <a name="character-map-transformation"></a>문자표 변환
  문자표 변환은 소문자에서 대문자로의 변환과 같은 문자열 함수를 문자 데이터에 적용합니다. 이 변환은 문자열 데이터 형식의 열 데이터에서만 실행됩니다.  
  
 문자표 변환은 사용 중인 열 데이터를 변환하거나 열을 변환 출력에 추가하고 변환된 데이터를 새 열에 배치할 수 있습니다. 다양한 매핑 작업 집합을 동일한 입력 열에 적용하고 결과를 다른 열에 배치할 수 있습니다. 예를 들어 동일한 열을 대문자와 소문자로 변환하고 결과를 두 개의 서로 다른 열에 배치할 수 있습니다.  
  
 매핑으로 인해 데이터가 잘리는 경우도 있습니다. 예를 들어 싱글바이트 문자를 멀티바이트 표현 문자로 매핑하면 데이터가 잘릴 수 있습니다. 문자표 변환에는 잘린 데이터를 별도의 출력으로 보내는 데 사용할 수 있는 오류 출력이 있습니다. 자세한 내용은 [데이터 오류 처리](../error-handling-in-data.md)를 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="mapping-operations"></a>매핑 작업  
 다음 표에서는 문자표 변환이 지원하는 매핑 작업을 설명합니다.  
  
|연산|Description|  
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
  
 **문자표 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Character Map Transformation Editor](../../character-map-transformation-editor.md)를 참조하십시오.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [변환 사용자 지정 속성](transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
