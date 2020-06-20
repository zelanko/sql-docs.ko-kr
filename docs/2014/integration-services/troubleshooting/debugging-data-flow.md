---
title: 데이터 흐름 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cc99e29d95aa08ce9363ca1fa6971d7602824868
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972773"
---
# <a name="debugging-data-flow"></a>데이터 흐름 디버깅
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 데이터 흐름 문제를 해결하는 데 사용할 수 있는 기능과 도구가 포함되어 있습니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 데이터 뷰어를 제공합니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변환은 행 개수를 확인합니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 런타임에 진행률을 보고합니다.  
  
## <a name="data-viewers"></a>데이터 뷰어  
 데이터 뷰어는 두 구성 요소 간 데이터를 데이터 흐름으로 표시합니다. 데이터 뷰어는 데이터 원본에서 데이터가 추출되어 처음으로 데이터 흐름에 들어갈 때, 변환으로 데이터가 업데이트되기 전/후와 데이터가 해당 대상으로 로드되기 전에 데이터를 표시합니다.  
  
 데이터를 보려면 두 데이터 흐름 구성 요소를 연결하는 경로에 데이터 뷰어를 연결합니다. 데이터 흐름 구성 요소 간의 데이터를 확인하면 예기치 않은 데이터 값을 확인하고, 변환으로 열 값이 변경되는 방식을 확인하고, 변환이 실패하는 이유를 확인하는 등의 작업을 더 쉽게 수행할 수 있습니다. 예를 들어 참조 테이블에서 실패한 조회를 확인하고 이를 수정하기 위해 빈 열에 대해 기본 데이터를 제공하는 변환을 추가할 수 있습니다.  
  
 데이터 뷰어는 표에 데이터를 표시할 수 있습니다. 표를 사용하면 표시할 열을 선택할 수 있습니다. 선택한 열의 값은 표 형식으로 표시됩니다.  
  
 또한 경로에 여러 데이터 뷰어를 포함시킬 수 있습니다. 동일 데이터를 여러 형식으로 표시하거나(예: 데이터의 차트 뷰 및 표 뷰 만들기) 데이터의 여러 열에 대해 서로 다른 데이터 뷰어를 만들 수 있습니다.  
  
 데이터 뷰어를 경로에 추가하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **데이터 흐름** 탭의 디자인 화면에서 경로 옆에 데이터 뷰어 아이콘을 추가합니다. 조건부 분할 변환과 같이 여러 출력을 포함할 수 있는 변환에는 각 경로에 데이터 뷰어가 포함될 수 있습니다.  
  
 런타임에 **데이터 뷰어** 창이 열리고 데이터 뷰어 형식으로 지정된 정보가 표시됩니다. 예를 들어 표 형식을 사용하는 데이터 뷰어는 선택된 열, 데이터 흐름 구성 요소로 전달된 출력 행의 수 및 표시된 행의 수에 대한 데이터를 표시합니다. 이 정보는 버퍼별로 표시되며 버퍼에 포함되는 행의 수는 데이터 흐름에서 행의 폭에 따라 결정됩니다.  
  
 **데이터 뷰어** 대화 상자에서 데이터를 클립보드로 복사하고, 테이블에서 모든 데이터를 삭제하고, 데이터 뷰어를 다시 구성하고, 데이터 흐름을 재개하고, 데이터 뷰어를 연결하거나 연결을 끊을 수 있습니다.  
  
#### <a name="to-add-a-data-viewer"></a>데이터 뷰어를 추가하려면  
  
-   [데이터 흐름에 데이터 뷰어 추가](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>행 개수  
 경로를 통해 전달된 행 개수가 **디자이너의** 데이터 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭의 디자인 화면에서 경로 옆에 표시됩니다. 데이터가 경로를 통해 이동하는 동안 개수가 주기적으로 업데이트됩니다.  
  
 또한 행 개수 변환을 데이터 흐름에 추가하여 변수에서 마지막 행 개수를 캡처할 수 있습니다. 자세한 내용은 [Row Count Transformation](../data-flow/transformations/row-count-transformation.md)을 참조하세요.  
  
## <a name="progress-reporting"></a>진행률 보고  
 패키지를 실행할 때 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 상태를 나타내는 색으로 각 데이터 흐름 구성 요소를 표시하여 **데이터 흐름** 탭의 디자인 화면에 진행률을 표시합니다. 각 구성 요소에서 해당 작업 수행을 시작하면 색이 노란색으로 바뀌고, 성공적으로 완료되면 녹색으로 바뀝니다. 빨간색은 구성 요소가 실패했음을 나타냅니다.  
  
 다음 표에서는 색 구분 기능에 대해 설명합니다.  
  
|색|Description|  
|-----------|-----------------|  
|색 없음|데이터 흐름 엔진의 호출을 대기 중입니다.|  
|노란색|변환 수행, 데이터 추출 또는 데이터 로드 중입니다.|  
|녹색|성공적으로 실행되었습니다.|  
|red|실행 중 오류가 발생했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [패키지 배포 문제 해결 도구](troubleshooting-tools-for-package-development.md)  
  
  
