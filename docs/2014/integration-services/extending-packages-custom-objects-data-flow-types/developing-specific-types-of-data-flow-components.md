---
title: 특정 유형의 데이터 흐름 구성 요소 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92c038a3d293b63682efbba62204ad335bf0ba12
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427910"
---
# <a name="developing-specific-types-of-data-flow-components"></a>특정 유형의 데이터 흐름 구성 요소 개발
  이 섹션에서는 원본 구성 요소, 동기 출력을 사용하는 변환 구성 요소, 비동기 출력을 사용하는 변환 구성 요소 및 대상 구성 요소를 개발할 때의 세부 사항에 대해 설명합니다.  
  
 구성 요소 개발에 대한 일반적인 정보는 [사용자 지정 데이터 흐름 구성 요소 개발](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 지정 원본 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 외부 데이터 원본의 데이터에 액세스하고 이 데이터를 데이터 흐름의 다운스트림 구성 요소에 제공하는 구성 요소를 개발하는 방법에 대한 정보를 제공합니다.  
  
 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 출력이 입력과 동기적으로 이루어지는 변환 구성 요소를 개발하는 방법에 대한 정보를 제공합니다. 이러한 구성 요소는 데이터를 데이터 흐름에 추가하는 것이 아니라 해당 데이터가 전달될 때 처리합니다.  
  
 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 출력이 입력과 동기적으로 이루어지지 않는 변환 구성 요소를 개발하는 방법에 대한 정보를 제공합니다. 이러한 구성 요소는 업스트림 구성 요소에서 데이터를 받고 데이터 흐름에 데이터를 추가합니다.  
  
 [사용자 지정 대상 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 데이터 흐름의 업스트림 구성 요소에서 행을 받고 이를 외부 데이터 원본에 쓰는 구성 요소를 개발하는 방법에 대한 정보를 제공합니다.  
  
## <a name="reference"></a>참조  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 사용자 지정 데이터 흐름 구성 요소를 만드는 데 사용되는 클래스와 인터페이스에 대해 설명합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 데이터 흐름 태스크의 관리되지 않는 클래스 및 인터페이스에 대해 설명합니다. 개발자는 프로그래밍 방식으로 데이터 흐름을 작성하거나 사용자 지정 데이터 흐름 구성 요소를 만들 때 이러한 클래스 및 인터페이스와 관리되는 <xref:Microsoft.SqlServer.Dts.Pipeline> 네임스페이스를 사용합니다.  
  
![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [스크립팅 솔루션과 사용자 지정 개체 비교](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [특정 유형의 스크립트 구성 요소 개발](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
