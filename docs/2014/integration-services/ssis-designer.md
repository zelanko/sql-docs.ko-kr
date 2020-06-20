---
title: SSIS 디자이너 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c930d9c75be324e920f4fa2a5368b20c14741bf0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962640"
---
# <a name="ssis-designer"></a>SSIS 디자이너
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만들고 유지 관리하는 데 사용할 수 있는 그래픽 도구입니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 프로젝트의 일부로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 사용할 수 있습니다.

 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 다음 태스크를 수행할 수 있습니다.

-   패키지의 제어 흐름 구성

-   패키지의 데이터 흐름 구성

-   패키지 및 패키지 개체에 이벤트 처리기 추가

-   패키지 내용 보기

-   런타임에 패키지의 실행 진행률 보기

 다음 다이어그램은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너와 **도구 상자** 창을 보여 줍니다.

 ![SSIS 디자이너 및 도구 상자의 스크린샷](media/denali-designerandtoolbox.gif "SSIS 디자이너 및 도구 상자의 스크린샷")

 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 패키지에 대한 추가 기능을 제공하는 추가 대화 상자 및 창이 있으며, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에는 개발 환경 구성 및 패키지 사용을 위한 창 및 대화 상자가 제공됩니다. 자세한 내용은 [Integration Services 사용자 인터페이스](integration-services-user-interface.md)를 참조하세요.

 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 패키지를 관리 및 모니터링하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 종속되지 않으며 서비스가 실행 중이 아니어도 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 만들거나 수정할 수 있습니다. 하지만 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너가 열려 있는 상태에서 서비스를 중지하면 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 제공하는 대화 상자를 열 수 없으며 "RPC 서버를 사용할 수 없습니다"와 같은 오류 메시지가 표시될 수 있습니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 다시 설정하고 패키지로 계속 작업하려면 디자이너를 닫고 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 종료한 다음 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트 및 패키지를 다시 열어야 합니다.

## <a name="undo-and-redo"></a>실행 취소 및 다시 실행
 [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer에서는 최대 20개의 동작을 실행 취소하고 다시 실행할 수 있습니다. 패키지의 경우 **제어 흐름**, **데이터 흐름**, **이벤트 처리기**및 **매개 변수** 탭과 **변수** 창에서 실행 취소/다시 실행을 사용할 수 있습니다. 프로젝트의 경우 **프로젝트 매개 변수** 창에서 실행 취소/다시 실행을 사용할 수 있습니다.

 새 **SSIS 도구 상자**의 변경 내용은 실행 취소/다시 실행할 수 없습니다.

 구성 요소 편집기를 사용하여 구성 요소를 변경할 때는 개별적으로 변경을 실행 취소하고 다시 실행하는 대신 집합으로 변경을 실행 취소하고 다시 실행합니다. 변경 집합은 실행 취소와 다시 실행 드롭다운 목록에서 단일 동작으로 나타납니다.

 동작을 실행 취소하려면 실행 취소 도구 모음 단추를 클릭하거나 **편집/실행 취소** 메뉴 항목을 선택하거나 Ctrl+Z를 누릅니다. 동작을 다시 실행하려면 다시 실행 도구 모음 단추를 클릭하거나 **편집/다시 실행** 메뉴 항목을 선택하거나 CTRL + Y를 누릅니다. 도구 모음 단추 옆의 화살표를 클릭하고 드롭다운 목록에서 여러 동작을 강조 표시한 다음 목록에서 클릭하여 여러 동작을 실행 취소하고 다시 실행할 수 있습니다.

## <a name="parts-of-the-ssis-designer"></a>SSIS 디자이너의 구성 요소
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에는 각각 패키지 제어 흐름, 데이터 흐름, 매개 변수 및 이벤트 처리기 구축을 위한 4개의 탭과 패키지 내용을 보기 위한 1개의 탭 등 총 5개의 영구적인 탭이 있습니다. 런타임에는 실행 중인 패키지의 실행 과정과 실행 후의 결과를 보여 주는 6번째 탭이 나타납니다.

 또한 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에는 패키지가 데이터에 연결하기 위해 사용하는 연결 관리자를 추가 및 구성하기 위한 연결 관리자 영역이 있습니다.

### <a name="control-flow-tab"></a>제어 흐름 탭
 **제어 흐름** 탭의 디자인 화면에서 패키지의 제어 흐름을 구성합니다. **도구 상자** 에서 디자인 화면으로 항목을 끌어다 놓고 항목 아이콘을 클릭한 후 한 항목에서 다른 항목으로 화살표를 끌어서 항목을 제어 흐름으로 연결합니다.

 자세한 내용은 [Control Flow](control-flow/control-flow.md)을 참조하세요.

### <a name="data-flow-tab"></a>데이터 흐름 탭
 패키지에 데이터 흐름 태스크가 포함된 경우 패키지에 데이터 흐름을 추가할 수 있습니다. **데이터 흐름** 탭의 디자인 화면에서 패키지의 데이터 흐름을 구성합니다. **도구 상자** 에서 디자인 화면으로 항목을 끌어 놓고 항목 아이콘을 클릭한 후 한 항목에서 다른 항목으로 화살표를 끌어서 항목을 데이터 흐름으로 연결합니다.

 자세한 내용은 [Data Flow](data-flow/data-flow.md)을 참조하세요.

### <a name="parameters-tab"></a>매개 변수 탭
 Integration Services(SSIS) 매개 변수를 사용하여 패키지 실행 시 패키지 내의 속성에 값을 할당할 수 있습니다. 프로젝트 수준에서 프로젝트 매개 변수를 만들고 패키지 수준에서 패키지 매개 변수를 만들 수 있습니다. 프로젝트 매개 변수는 프로젝트가 수신하는 외부 입력을 프로젝트 내 하나 이상의 패키지에 제공하기 위해 사용됩니다. 패키지 매개 변수를 사용하면 패키지를 편집하여 다시 배포할 필요 없이 패키지 실행을 수정할 수 있습니다. 이 탭에서 패키지 매개 변수를 관리할 수 있습니다.

 매개 변수에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 매개 변수](integration-services-ssis-package-and-project-parameters.md)를 참조하세요.

> [!IMPORTANT]
>  매개 변수는 프로젝트 배포 모델을 위해 배포된 프로젝트에만 사용할 수 있습니다. 따라서 프로젝트 배포 모델을 사용하도록 구성된 프로젝트에 속한 패키지에 대해서만 매개 변수 탭이 표시됩니다.

### <a name="event-handlers-tab"></a>이벤트 처리기 탭
 **이벤트 처리기** 탭의 디자인 화면에서 패키지의 이벤트를 생성 합니다. **이벤트 처리기 탭에서** 이벤트 처리기를 만들려는 패키지 또는 패키지 개체를 선택한 다음 이벤트 처리기와 연결할 이벤트를 선택 합니다. 이벤트 처리기에는 제어 흐름과 선택적 데이터 흐름이 있습니다.

 자세한 내용은 [Add an Event Handler to a Package](../../2014/integration-services/add-an-event-handler-to-a-package.md)을(를) 참조하세요.

### <a name="package-explorer-tab"></a>패키지 탐색기 탭
 패키지는 여러 태스크, 연결 관리자, 변수 및 기타 요소가 포함되어 복잡할 수 있습니다. 패키지를 탐색기로 보면 전체 패키지 요소 목록을 확인할 수 있습니다.

 자세한 내용은 [패키지 개체 보기](view-package-objects.md)를 참조하세요.

#### <a name="progressexecution-result-tab"></a>진행률/실행 결과 탭
 패키지가 실행 중인 동안 **진행률** 탭에는 패키지의 실행 진행률이 표시됩니다. 패키지 실행이 종료되면 **실행 결과** 탭에서 실행 결과를 확인할 수 있습니다.

> [!NOTE]
>  **진행률** 탭에 메시지를 표시할지 여부는 **SSIS** 메뉴의 **디버그 진행률 보고** 옵션을 선택 또는 선택 취소하여 설정합니다.

##### <a name="connection-managers-area"></a>연결 관리자 영역
 **연결 관리자** 영역에서는 패키지에서 사용되는 연결 관리자를 추가하고 수정합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 텍스트 파일, OLE DB 데이터베이스 및 .NET 공급자와 같은 다양한 데이터 원본에 연결하기 위한 연결 관리자가 포함됩니다.

 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](connection-manager/integration-services-ssis-connections.md) 및 [연결 관리자 만들기](../../2014/integration-services/create-connection-managers.md)를 참조하세요.

## <a name="related-tasks"></a>관련 작업

-   [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md)

## <a name="see-also"></a>참고 항목
 [Integration Services 사용자 인터페이스](integration-services-user-interface.md)


