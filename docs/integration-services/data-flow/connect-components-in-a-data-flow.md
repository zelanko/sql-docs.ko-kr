---
title: 데이터 흐름의 구성 요소 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d075cb578046862c4598efd9da3c060891ae7a7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045293"
---
# <a name="connect-components-in-a-data-flow"></a>데이터 흐름의 구성 요소 연결

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 절차에서는 데이터 흐름의 구성 요소 출력을 동일 데이터 흐름 내의 다른 구성 요소에 연결하는 방법에 대해 설명합니다.  
**디자이너의** 데이터 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭의 디자인 화면에서 패키지의 데이터 흐름을 구성합니다. 데이터 흐름에 데이터 흐름 구성 요소가 두 개 있으면 원본 또는 변환의 출력을 변환 또는 대상의 입력에 연결하여 두 구성 요소를 연결할 수 있습니다. 두 데이터 흐름 구성 요소 간 연결선을 경로라고 합니다.  
  
 다음 다이어그램에서는 하나의 원본 구성 요소, 두 개의 변환, 하나의 대상 구성 요소 및 이를 연결하는 경로가 포함된 간단한 데이터 흐름을 보여 줍니다.  
  
 ![Data flow](../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 두 구성 요소를 연결한 다음에는 **데이터 흐름 경로 편집기**에서 경로를 통해 이동하는 데이터의 메타데이터와 경로의 속성을 볼 수 있습니다. 자세한 내용은 [Integration Services Paths](../../integration-services/data-flow/integration-services-paths.md)을(를) 참조하세요.  
  
 경로에 데이터 뷰어를 추가할 수도 있습니다. 데이터 뷰어를 사용하면 패키지가 실행될 때 데이터 흐름 구성 요소 간에 이동하는 데이터를 볼 수 있습니다.  
  
### <a name="connect-components-in-a-data-flow"></a>데이터 흐름의 구성 요소 연결  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 구성 요소를 연결하려는 데이터 흐름이 들어 있는 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  **데이터 흐름** 탭의 디자인 화면에서 연결하려는 변환 또는 원본을 선택합니다.  
  
5.  변환 또는 원본의 녹색 출력 화살표를 변환 또는 대상으로 끌어 옵니다. 일부 데이터 흐름 구성 요소에는 오류 출력이 포함되어 있으며 이 출력도 동일한 방법으로 연결할 수 있습니다.  
  
    > [!NOTE]  
    >  일부 데이터 흐름 구성 요소에는 여러 출력이 포함될 수 있으며 각 출력을 서로 다른 변환이나 대상으로 연결할 수 있습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름에서 구성 요소 추가 또는 삭제](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [데이터 흐름 디버깅](../../integration-services/troubleshooting/debugging-data-flow.md) [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
