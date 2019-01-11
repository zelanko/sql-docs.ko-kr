---
title: Integration Services(SSIS) 이벤트 처리기 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- run-time [Integration Services]
- SQL Server Integration Services packages, events
- event handlers [Integration Services], about event handlers
- events [Integration Services]
- packages [Integration Services], events
- event handlers [Integration Services]
- SSIS packages, events
- containers [Integration Services], events
- events [Integration Services], about events
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3d7ea5c6424283bd7b8aaa44f8a026ea18a9db30
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751125"
---
# <a name="integration-services-ssis-event-handlers"></a>Integration Services(SSIS) 이벤트 처리기
  런타임 시 실행 개체(패키지 및 Foreach 루프, For 루프, 시퀀스 및 태스크 호스트 컨테이너)는 이벤트를 발생시킵니다. 예를 들어 오류가 발생하면 OnError 이벤트가 발생합니다. 이러한 이벤트에 대한 사용자 지정 이벤트 처리기를 만들면 패키지 기능을 확장하고 런타임 시 패키지를 더 쉽게 관리할 수 있습니다. 이벤트 처리기는 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   패키지 또는 태스크 실행이 완료될 때 임시 데이터 스토리지를 삭제합니다.  
  
-   패키지 실행 전에 리소스 사용 가능 여부를 확인하기 위해 시스템 정보를 검색합니다.  
  
-   참조 테이블에서 조회가 실패하는 경우 테이블의 데이터를 새로 고칩니다.  
  
-   오류 또는 경고가 발생하거나 태스크가 실패하는 경우 전자 메일 메시지를 보냅니다.  
  
 이벤트에 이벤트 처리기가 없으면 패키지의 컨테이너 계층에서 다음 순서의 컨테이너로 이벤트가 전달됩니다. 이 컨테이너에 이벤트 처리기가 있으면 이벤트에 대한 응답으로 이 이벤트 처리기가 실행됩니다. 그렇지 않으면 이벤트가 다시 컨테이너 계층에서 다음 순서의 컨테이너로 전달됩니다.  
  
 다음 다이어그램은 하나의 SQL 실행 태스크가 포함된 For 루프 컨테이너가 들어 있는 간단한 패키지를 보여 줍니다.  
  
 ![패키지, For 루프, 태스크 호스트 및 SQL 실행 태스크](media/mw-dts-eventhandlerpkg.gif "패키지, For 루프, 태스크 호스트 및 SQL 실행 태스크")  
  
 이 패키지에는 `OnError` 이벤트에 대한 이벤트 처리기만 들어 있습니다. SQL 실행 태스크가 실행될 때 오류가 발생하면 패키지에 대한 `OnError` 이벤트 처리기가 실행됩니다. 다음 다이어그램은 `OnError` 이벤트 처리기가 패키지를 실행하도록 만드는 호출 시퀀스를 보여 줍니다.  
  
 ![이벤트 처리기 흐름](media/mw-dts-eventhandlers.gif "이벤트 처리기 흐름")  
  
 이벤트 처리기는 이벤트 처리기 컬렉션의 멤버이며 모든 컨테이너에는 이 컬렉션이 포함됩니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 만드는 경우에는 **디자이너의** 패키지 탐색기 **탭에 있는** 이벤트 처리기 [!INCLUDE[ssIS](../includes/ssis-md.md)] 폴더에서 이벤트 처리기 컬렉션의 멤버를 확인할 수 있습니다.  
  
 다음과 같은 방법으로 이벤트 처리기 컨테이너를 구성할 수 있습니다.  
  
-   이벤트 처리기에 대한 이름 및 설명을 지정합니다.  
  
-   이벤트 처리기 실행 여부, 이벤트 처리기 실패 시 패키지가 실패하는지 여부 및 이벤트 처리기 실패 시 발생할 수 있는 오류 개수를 나타냅니다.  
  
-   이벤트 처리기가 런타임에 반환하는 실제 실행 결과 대신 반환할 실행 결과를 지정합니다.  
  
-   이벤트 처리기의 트랜잭션 옵션을 지정합니다.  
  
-   이벤트 처리기에서 사용되는 로깅 모드를 지정합니다.  
  
## <a name="event-handler-content"></a>이벤트 처리기 내용  
 이벤트 처리기를 만드는 방법은 패키지를 빌드하는 방법과 비슷합니다. 이벤트 처리기에는 제어 흐름으로 순서가 지정된 태스크 및 컨테이너가 포함되며, 데이터 흐름이 포함될 수도 있습니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에는 사용자 지정 이벤트 처리기를 만들기 위한 **이벤트 처리기** 탭이 포함됩니다. 자세한 내용은 [SSIS 패키지 이벤트 처리기](integration-services-ssis-event-handlers.md)합니다.  
  
 이벤트 처리기를 프로그래밍 방식으로 만들 수도 있습니다. 자세한 내용은 [프로그래밍 방식으로 이벤트 처리](building-packages-programmatically/handling-events-programmatically.md)를 참조하세요.  
  
## <a name="run-time-events"></a>런타임 이벤트  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 제공되는 이벤트 처리기를 나열하고 이벤트 처리기를 실행하는 런타임 이벤트에 대해 설명합니다.  
  
|이벤트 처리기|이벤트|  
|-------------------|-----------|  
|`OnError`|에 대 한 이벤트 처리기는 `OnError` 이벤트입니다. 이 이벤트는 오류가 발생할 때 실행 개체에 의해 발생합니다.|  
|**OnExecStatusChanged**|**OnExecStatusChanged** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 실행 상태가 변경될 때 실행 개체에 의해 발생합니다.|  
|**OnInformation**|**OnInformation** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 정보 보고를 위한 실행 개체의 유효성 검사 및 실행 중에 발생합니다. 이 이벤트에는 오류 또는 경고를 제외한 정보만 포함됩니다.|  
|**OnPostExecute**|**OnPostExecute** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 실행을 마친 바로 다음 실행 개체에 의해 발생합니다.|  
|**OnPostValidate**|**OnPostValidate** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 유효성 검사가 완료될 때 실행 개체에 의해 발생합니다.|  
|**OnPreExecute**|**OnPreExecute** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 실행되기 바로 전에 실행 개체에 의해 발생합니다.|  
|**OnPreValidate**|**OnPreValidate** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 유효성 검사가 시작될 때 실행 개체에 의해 발생합니다.|  
|**OnProgress**|**OnProgress** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 실행 개체의 진행 상태를 측정할 수 있는 경우 실행 개체에 의해 발생합니다.|  
|**OnQueryCancel**|**OnQueryCancel** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 실행 중지 시기를 결정하기 위해 실행 개체에 의해 발생합니다.|  
|**OnTaskFailed**|**OnTaskFailed** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 작업이 실패할 때 해당 태스크에 의해 발생합니다.|  
|**OnVariableValueChanged**|**OnVariableValueChanged** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 변수 값이 변경될 때 실행 개체에 의해 발생합니다. 이 이벤트는 변수가 정의되는 실행 개체에 의해 발생합니다. 설정 하는 경우이 이벤트가 발생 하지 않습니다 합니다 **RaiseChangeEvent** 변수를 속성 `False`합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)을 참조하세요.|  
|**OnWarning**|**OnWarning** 이벤트에 대한 이벤트 처리기입니다. 이 이벤트는 경고가 발생할 때 실행 개체에 의해 발생합니다.|  
  
## <a name="configuration-of-an-event-handler"></a>이벤트 처리기 구성  
 **의** 속성 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 창을 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)을 참조하세요.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 패키지에 이벤트 처리기를 추가하는 방법에 대한 자세한 내용은 [패키지에 이벤트 처리기 추가](../../2014/integration-services/add-an-event-handler-to-a-package.md)를 참조하세요.  
  
  
