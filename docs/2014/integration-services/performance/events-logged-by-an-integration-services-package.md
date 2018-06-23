---
title: Integration Services 패키지에서 기록하는 이벤트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4e13833f583f7afb903d16fabe7a72ce66bf1e4a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093352"
---
# <a name="events-logged-by-an-integration-services-package"></a>통합 서비스 패키지에 의해 기록된 이벤트
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 Windows 응용 프로그램 로그에 다양한 이벤트 메시지를 기록합니다. 이러한 메시지는 패키지가 시작되거나 중지될 때 또는 특정 문제가 발생할 때 기록됩니다.  
  
 이 항목에서는 패키지가 응용 프로그램 이벤트 로그에 기록하는 일반적인 이벤트 메시지에 대해 설명합니다. 이러한 메시지 중 일부는 패키지에 로깅이 사용되도록 설정되지 않은 경우에도 기본적으로 기록되지만 일부 메시지는 패키지에 로깅이 사용되도록 설정된 경우에만 기록됩니다. 패키지가 이러한 메시지를 기본적으로 기록하는지 아니면 로깅이 사용되도록 설정되어 있기 때문에 기록하는지 여부에 관계없이 메시지의 이벤트 원본은 SQLISPackage입니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하는 방법에 대한 일반적인 내용은 [프로젝트 및 패키지 실행](../packages/run-integration-services-ssis-packages.md)을 참조하세요.  
  
 패키지 실행 문제를 해결하는 방법에 대한 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="messages-about-the-status-of-the-package"></a>패키지의 상태에 대한 메시지  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하면 일반적으로 패키지의 진행률과 상태에 대한 다양한 메시지가 기록됩니다. 다음 표에서는 이러한 메시지를 나열합니다.  
  
> [!NOTE]  
>  다음 표에 나열된 메시지는 패키지에 로깅이 사용되도록 설정되지 않은 경우에도 기록됩니다.  
  
|이벤트 ID|심볼 이름|텍스트 모드|참고|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|패키지 ""이(가) 시작되었습니다.|패키지의 실행이 시작되었습니다.|  
|12289|DTS_MSG_PACKAGESUCCESS|패키지 ""이(가) 성공적으로 완료되었습니다.|패키지가 성공적으로 실행되었고 더 이상 실행 중이지 않습니다.|  
|12290|DTS_MSG_PACKAGECANCEL|패키지 "%1!s!"이(가) 취소되었습니다.|패키지가 취소되었기 때문에 더 이상 실행 중이지 않습니다.|  
|12291|DTS_MSG_PACKAGEFAILURE|패키지 ""이(가) 실패했습니다.|패키지가 성공적으로 실행되지 못했고 실행이 중지되었습니다.|  
  
 기본적으로 새로 설치하는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 실행과 관련된 특정 이벤트를 응용 프로그램 이벤트 로그에 기록하지 않도록 구성됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]현재 릴리스의 데이터 수집기 기능을 사용하는 경우 이 설정은 이벤트 로그 항목이 너무 많이 생성되지 않도록 방지합니다. 기록되지 않는 이벤트는 EventID 12288, "패키지가 시작되었습니다" 및 EventID 12289, "패키지가 성공적으로 완료되었습니다"입니다. 이러한 이벤트를 응용 프로그램 이벤트 로그에 기록하려면 편집을 위해 레지스트리를 엽니다. 그런 다음 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS 노드를 찾고 LogPackageExecutionToEventLog 설정의 DWORD 값을 0에서 1로 변경합니다. 그러나 업그레이드 설치에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 이러한 두 이벤트를 기록하도록 구성됩니다. 로깅을 사용하지 않으려면 LogPackageExecutionToEventLog 설정의 값을 1에서 0으로 변경합니다.  
  
## <a name="messages-associated-with-package-logging"></a>패키지 로깅과 관련된 메시지  
 패키지에 로깅이 사용되도록 설정된 경우 응용 프로그램 이벤트 로그는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 선택적 로깅 기능이 지원하는 대상 중 하나입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](integration-services-ssis-logging.md)을 참조하세요.  
  
 패키지에 로깅이 사용되도록 설정되어 있고 로그 위치가 응용 프로그램 이벤트 로그인 경우 패키지는 다음 정보와 관련된 항목을 기록합니다.  
  
-   패키지가 실행될 때 패키지가 위치한 단계에 대한 메시지  
  
-   패키지가 실행될 때 발생하는 특정 이벤트에 대한 메시지  
  
### <a name="messages-about-the-stages-of-package-execution"></a>패키지 실행 단계에 대한 메시지  
  
|이벤트 ID|심볼 이름|텍스트 모드|참고|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|응용 프로그램 이벤트 로그에 메시지를 기록하도록 패키지를 구성한 경우 다양한 메시지에서 이 일반 형식을 사용합니다.|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|패키지가 시작되었습니다.|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|개체에 대한 유효성 검사가 시작되려고 합니다.|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|개체에 대한 유효성 검사가 완료되었습니다.|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|이 일반 메시지는 패키지 진행률을 보고합니다.|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|개체가 해당 작업을 완료했습니다.|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|패키지의 실행이 완료되었습니다.|  
  
### <a name="messages-about-events-that-occur"></a>발생한 이벤트에 대한 메시지  
 다음 표에서는 이벤트의 결과인 일부 메시지만 나열합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용하는 오류, 경고 및 정보 메시지의 보다 포괄적인 목록은 [Integration Services 오류 및 메시지 참조](../integration-services-error-and-message-reference.md)를 참조하세요.  
  
|이벤트 ID|심볼 이름|텍스트 모드|참고|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|태스크가 실패했습니다.|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|이 메시지는 발생한 오류를 보고합니다.|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|이 메시지는 발생한 경고를 보고합니다.|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|이벤트 이름: %1%r 메시지: %9%r 연산자: %2%r 원본 이름: %3%r 원본 ID: %4%r 실행 ID: %5%r 시작 시간: %6%r 종료 시간: %7%r 데이터 코드: %8|이 메시지는 오류 또는 경고와 관련 없는 정보를 보고합니다.|  
  
## <a name="related-tasks"></a>관련 작업  
 실시간으로 로그 항목을 보는 방법에 대한 자세한 내용은 [이벤트 로그 창에서 로그 항목 보기](../view-log-entries-in-the-log-events-window.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서비스에서 기록하는 이벤트](../service/events-logged-by-the-integration-services-service.md)  
  
  