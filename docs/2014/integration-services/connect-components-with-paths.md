---
title: 경로를 사용 하 여 구성 요소 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8d6cc5a5fb14fff5fd92d5120f56c06d57ddcbaf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921394"
---
# <a name="connect-components-with-paths"></a>경로에 구성 요소 연결
  **디자이너의** 데이터 흐름 [!INCLUDE[ssIS](../includes/ssis-md.md)] 탭의 디자인 화면에서 패키지의 데이터 흐름을 구성합니다. 데이터 흐름에 데이터 흐름 구성 요소가 두 개 있으면 원본 또는 변환의 출력을 변환 또는 대상의 입력에 연결하여 두 구성 요소를 연결할 수 있습니다. 두 데이터 흐름 구성 요소 간 연결선을 경로라고 합니다.

 다음 다이어그램에서는 하나의 원본 구성 요소, 두 개의 변환, 하나의 대상 구성 요소 및 이를 연결하는 경로가 포함된 간단한 데이터 흐름을 보여 줍니다.

 ![데이터 흐름](media/mw-dts-08.gif "데이터 흐름")

 두 구성 요소를 연결한 다음에는 **데이터 흐름 경로 편집기**에서 경로를 통해 이동하는 데이터의 메타데이터와 경로의 속성을 볼 수 있습니다. 자세한 내용은 [Integration Services Paths](data-flow/integration-services-paths.md)을(를) 참조하세요.

 경로에 데이터 뷰어를 추가할 수도 있습니다. 데이터 뷰어를 사용하면 패키지가 실행될 때 데이터 흐름 구성 요소 간에 이동하는 데이터를 볼 수 있습니다.

### <a name="to-connect-components-in-a-data-flow"></a>데이터 흐름에서 구성 요소를 연결하려면

-   [데이터 흐름의 구성 요소 연결](data-flow/connect-components-in-a-data-flow.md)

### <a name="to-set-path-properties"></a>경로 속성을 설정하려면

-   [데이터 흐름 경로 편집기를 사용하여 경로의 속성 설정](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)

### <a name="to-view-path-metadata"></a>경로 메타데이터를 보려면

-   [데이터 흐름 경로 편집기를 사용하여 경로 메타데이터 보기](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)

### <a name="to-view-path-metadata"></a>경로 메타데이터를 보려면

-   [데이터 흐름에 데이터 뷰어 추가](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)

## <a name="see-also"></a>참고 항목
 데이터 [흐름 태스크](control-flow/data-flow-task.md) 데이터 [흐름](data-flow/data-flow.md) [변환](data-flow/transformations/transform-data-with-transformations.md) 데이터의 변환 [오류 처리](data-flow/error-handling-in-data.md)


