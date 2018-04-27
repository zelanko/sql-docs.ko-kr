---
title: 프로그래밍 방식으로 패키지 작성 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: building-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 721de0871951dfb88742c325588ea4147b3a33b9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="building-packages-programmatically"></a>프로그래밍 방식으로 패키지 작성
  패키지를 동적으로 만들거나 개발 환경 외부에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리 및 실행해야 하는 경우 패키지를 프로그래밍 방식으로 조작할 수 있습니다. 이 경우 다음 중 하나를 선택할 수 있습니다.  
  
-   기존 패키지를 로드하고 수정하지 않은 채로 실행합니다.  
  
-   기존 패키지를 로드하고 다시 구성(예를 들어 다른 데이터 원본에 사용할 수 있도록 구성)한 다음 실행합니다.  
  
-   새 패키지를 만들고 구성 요소를 개체별 및 속성별로 구성한 다음 새 패키지를 저장 후 실행합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델을 사용하면 패키지를 만들고 구성하고 실행하는 코드를 관리되는 프로그래밍 언어로 작성할 수 있습니다. 예를 들어 선택한 데이터 원본과 해당 데이터 원본의 테이블 및 열을 기반으로 연결이나 데이터 원본, 변환 및 대상을 구성하는 메타데이터 구동 패키지를 만들 수 있습니다.  
  
 이 섹션에서는 패키지를 프로그래밍 방식으로 한 줄씩 만들고 구성하는 방법을 설명하고 예로 보여 줍니다. 위에 나열된 패키지 프로그래밍 방법 중 비교적 덜 복잡한 첫 번째 방법은 [프로그래밍 방식으로 패키지 실행 및 관리](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)에 설명된 대로 단순히 기존 패키지를 로드한 다음 수정하지 않은 채 실행하는 것입니다.  
  
 두 번째 방법은 여기에서는 설명하지 않지만 기존 패키지를 템플릿으로 로드하고 다시 구성(예를 들어 다른 데이터 원본에 사용할 수 있도록 구성)한 다음 실행하는 것입니다. 이 섹션의 정보를 사용하여 패키지의 기존 개체를 수정할 수도 있습니다.  
  
> [!NOTE]  
>  기존 패키지를 템플릿으로 사용하고 데이터 흐름의 기존 열을 수정할 경우 기존 열을 제거하고 영향을 받는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 메서드를 호출해야 할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [프로그래밍 방식으로 패키지 만들기](../../integration-services/building-packages-programmatically/creating-a-package-programmatically.md)  
 프로그래밍 방식으로 패키지를 만드는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 태스크 추가](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
 패키지에 태스크를 추가하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 태스크 연결](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
 이전 태스크 또는 컨테이너의 실행 결과에 따라 패키지에서의 컨테이너 및 태스크 실행을 제어하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)  
 패키지에 연결 관리자를 추가하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 변수 작업](../../integration-services/building-packages-programmatically/working-with-variables-programmatically.md)  
 패키지 실행 중 변수를 추가하고 사용하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 이벤트 처리](../../integration-services/building-packages-programmatically/handling-events-programmatically.md)  
 패키지 및 태스크 이벤트를 처리하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 로깅 설정](../../integration-services/building-packages-programmatically/enabling-logging-programmatically.md)  
 패키지 또는 태스크에 대해 로깅 기능을 사용하도록 설정하는 방법과 로그 이벤트에 사용자 지정 필터를 적용하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 데이터 흐름 태스크 추가](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
 데이터 흐름 태스크 및 해당 구성 요소를 추가하고 구성하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 데이터 흐름 구성 요소 검색](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
 로컬 컴퓨터에 설치되어 있는 구성 요소를 검색하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 데이터 흐름 구성 요소 추가](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
 데이터 흐름 태스크에 구성 요소를 추가하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 데이터 흐름 구성 요소 연결](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
 두 개의 데이터 흐름 구성 요소를 연결하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 입력 열 선택](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
 데이터 흐름의 업스트림 구성 요소에서 구성 요소에 제공한 입력 열 중에서 입력 열을 선택하는 방법을 설명합니다.  
  
 [프로그래밍 방식으로 패키지 저장](../../integration-services/building-packages-programmatically/saving-a-package-programmatically.md)  
 패키지를 프로그래밍 방식으로 저장하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [스크립팅을 사용한 패키지 확장](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 스크립트 태스크를 사용하여 제어 흐름을 확장하는 방법과 스크립트 구성 요소를 사용하여 데이터 흐름을 확장하는 방법에 대해 설명합니다.  
  
 [사용자 지정 개체를 사용한 패키지 확장](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 여러 패키지에서 사용할 프로그램 사용자 지정 태스크, 데이터 흐름 구성 요소 및 기타 패키지 개체를 만드는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 실행 및 관리](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 패키지 및 패키지가 저장된 폴더를 열거하고 실행하고 관리하는 방법에 대해 설명합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   www.codeplex.com/MSFTISProdSamples의 CodePlex 예제 - [Integration Services 제품 예제](http://go.microsoft.com/fwlink/?LinkID=131204)  
  
-   blogs.msdn.com의 블로그 항목 - [사용자 지정 확장 프로그램 성능 프로파일링](http://go.microsoft.com/fwlink/?LinkId=238831)  

## <a name="see-also"></a>참고 항목  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
