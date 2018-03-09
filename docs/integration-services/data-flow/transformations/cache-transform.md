---
title: "캐시 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
- sql13.dts.designer.cachetrans.f1
- sql13.dts.designer.cachetranscon.f1
- sql13.dts.designer.cachetransmap.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83d157914c7090273a213a7f2ed4b6e5ea7f2fa5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="cache-transform"></a>캐시 변환
  캐시 변환은 데이터 흐름에 있는 연결된 데이터 원본의 데이터를 캐시 연결 관리자에 기록하여 조회 변환에 대한 참조 데이터 집합을 생성합니다. 조회 변환은 연결된 데이터 원본의 입력 열에 있는 데이터를 참조 데이터베이스의 열과 조인하여 조회합니다.  
  
 캐시 연결 관리자를 사용하여 조회 변환을 전체 캐시 모드로 실행하도록 구성할 수 있습니다. 이 모드에서 조회 변환이 실행되기 전에 참조 데이터 집합이 캐시에 로드됩니다.  
  
 캐시 연결 관리자 및 캐시 변환을 사용하여 전체 캐시 모드에서 조회 변환을 구성하는 방법에 대한 지침은 [캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)을 참조하세요.  
  
 참조 데이터 집합을 캐시하는 방법은 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
> [!NOTE]  
>  캐시 변환은 고유한 행만 캐시 연결 관리자에 기록합니다.  
  
 단일 패키지에서는 하나의 캐시 변환만 동일한 캐시 연결 관리자에 데이터를 기록할 수 있습니다. 패키지에 여러 캐시 변환이 포함된 경우에는 패키지가 실행될 때 호출되는 첫 번째 캐시 변환이 데이터를 연결 관리자에 기록합니다. 이후 캐시 변환의 쓰기 작업은 실패합니다.  
  
 자세한 내용은 [캐시 연결 관리자](../../../integration-services/data-flow/transformations/cache-connection-manager.md)를 참조하세요.  
  
## <a name="configuration-of-the-cache-transform"></a>캐시 변환 구성  
 데이터를 캐시 파일(.caw)에 저장하도록 캐시 연결 관리자를 구성할 수 있습니다.  
  
 다음과 같은 방법으로 캐시 변환을 구성할 수 있습니다.  
  
-   캐시 연결 관리자를 지정합니다.  
  
-   캐시 변환의 입력 열을 캐시 연결 관리자의 대상 열에 매핑합니다.  
  
    > [!NOTE]  
    >  각 입력 열은 대상 열로 매핑되어야 하며 열 데이터 형식이 일치해야 합니다. 그렇지 않으면 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 디자이너에서 오류 메시지를 표시합니다.  
  
     **캐시 연결 관리자 편집기** 를 사용하여 열 데이터 형식, 이름 및 다른 열 속성을 수정할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 디자이너에서 속성을 설정할 수 있습니다. **고급 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하십시오.  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="cache-transformation-editor-connection-manager-page"></a>캐시 변환 편집기(연결 관리자 페이지)
  **캐시 변환 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 기존 캐시 연결 관리자를 선택하거나 새 연결을 만들 수 있습니다.  
  
 캐시 연결 관리자에 대한 자세한 내용은 [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>변수  
 **Cache connection manager**  
 목록을 사용하여 기존 캐시 연결 관리자를 선택하거나 **새로 만들기** 단추를 사용하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 캐시 연결 관리자 편집기 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **편집**  
 기존 연결을 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)  
  
  
