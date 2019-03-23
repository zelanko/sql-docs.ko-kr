---
title: 연결 관리자 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef2ea7fa43556f0c4f12ee41101aedf396a23382
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374091"
---
# <a name="create-connection-managers"></a>연결 관리자 만들기
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 태스크를 여러 유형의 서버 및 데이터 원본에 연결하기 위한 다양한 연결 관리자가 포함됩니다. 연결 관리자는 여러 유형의 데이터 저장소에서 데이터를 추출하고 로드하는 데이터 흐름 구성 요소와 서버, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블 또는 파일에 로그를 기록하는 로그 공급자에서 사용됩니다. 예를 들어 메일 보내기 태스크가 포함된 패키지에서는 SMTP 연결 관리자 유형을 사용하여 SMTP(Simple Mail Transfer Protocol) 서버에 연결합니다. SQL 실행 태스크가 포함된 패키지에서는 OLE DB 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 연결할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
 새 연결 관리자를 만들 때 연결 관리자를 자동으로 만들고 구성하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 사용할 수 있습니다. 또한 마법사는 연결 관리자를 사용하는 원본과 대상을 만들고 구성할 수 있도록 도와줍니다. 자세한 내용은 [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)을 참조하세요.  
  
 수동으로 새 연결 관리자를 만들고 기존 패키지에 이 연결 관리자를 추가하려면 **디자이너의** 제어 흐름 **,** 데이터 흐름 **및**이벤트 처리기 **탭에 나타나는** 연결 관리자 [!INCLUDE[ssIS](../includes/ssis-md.md)] 영역을 사용합니다. **연결 관리자** 영역에서 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너가 제공하는 대화 상자를 사용하여 만들 연결 관리자 유형을 선택한 다음 해당 연결 관리자의 속성을 설정합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "연결 관리자 영역 사용" 섹션을 참조하십시오.  
  
 패키지에 연결 관리자를 추가한 다음에는 태스크, Foreach 루프 컨테이너, 원본, 변환 및 대상에서 연결 관리자를 사용할 수 있습니다. 자세한 내용은 [Integration Services 태스크](control-flow/integration-services-tasks.md), [Foreach 루프 컨테이너](control-flow/foreach-loop-container.md) 및 [데이터 흐름](data-flow/data-flow.md)을 참조하세요.  
  
## <a name="using-the-connection-managers-area"></a>연결 관리자 영역 사용  
 **디자이너의**제어 흐름 **,** 데이터 흐름 **또는** 이벤트 처리기 [!INCLUDE[ssIS](../includes/ssis-md.md)] 탭이 활성화된 상태에서 연결 관리자를 만들 수 있습니다.  
  
 다음 다이어그램은 **디자이너의** 제어 흐름 **탭에 표시된** 연결 관리자 [!INCLUDE[ssIS](../includes/ssis-md.md)] 영역을 보여 줍니다.  
  
 ![패키지가 포함된 제어 흐름 디자이너의 스크린샷](media/samplecontrolflow.gif "패키지가 포함된 제어 흐름 디자이너의 스크린샷")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>SSIS 디자이너에서 연결 관리자를 추가, 구성 또는 삭제하려면  
  
-   [패키지에서 연결 관리자 추가, 삭제 또는 공유](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [연결 관리자의 속성 설정](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>연결 관리자의 32비트 및 64비트 공급자  
 연결 관리자에서 사용하는 공급자는 대부분 32비트 및 64비트 버전에서 사용할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 디자인 환경은 32비트 환경이므로 패키지를 디자인하는 동안 32비트 공급자만 표시됩니다. 따라서 특정 공급자의 32비트 버전과 64비트 버전이 모두 설치되어 있는 경우 연결 관리자에서 64비트 버전을 사용하도록 구성할 수 있습니다.  
  
 런타임 시 올바른 버전이 사용되므로 디자인 타임에 32비트 버전의 공급자를 지정했어도 문제가 되지 않습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지가 실행될 경우에도 64비트 버전의 공급자를 실행할 수 있습니다.  
  
 두 버전의 공급자는 동일한 ID를 갖습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 런타임에서 사용 가능한 64비트 버전의 공급자를 사용하도록 할지 여부를 지정하려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 Run64BitRuntime 속성을 설정합니다. Run64BitRuntime 속성이로 설정 되어 있으면 `true`, 런타임에 찾아 Run64BitRuntime 경우 64 비트 공급자를 사용 하 여 `false`, 런타임에 찾아 32 비트 공급자를 사용 합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에서 설정할 수 있는 속성에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 및 Studio 환경](integration-services-ssis-development-and-management-tools.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [제어 흐름](control-flow/control-flow.md)   
 [데이터 흐름](data-flow/data-flow.md)   
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](integration-services-ssis-event-handlers.md)  
  
  
