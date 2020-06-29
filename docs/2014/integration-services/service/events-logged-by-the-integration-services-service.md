---
title: Integration Services 서비스에서 기록하는 이벤트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70649de39a1eb3ef699b8d0521324eeefa7d5cda
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421860"
---
# <a name="events-logged-by-the-integration-services-service"></a>Integration Services 서비스에서 기록하는 이벤트
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 Windows 애플리케이션 로그에 다양한 메시지를 기록합니다. 이러한 메시지는 서비스가 시작되거나 중지될 때 또는 특정 문제가 발생할 때 기록됩니다.  
  
 이 항목에서는 서비스가 애플리케이션 이벤트 로그에 기록하는 일반적인 이벤트 메시지에 대해 설명합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 SQLISService의 이벤트 원본을 사용하여 이 항목에서 설명하는 모든 메시지를 기록합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 일반적인 정보는 [Integration Services 서비스&#40;SSIS 서비스&#41;](integration-services-service-ssis-service.md)를 참조하세요.  
  
## <a name="messages-about-the-status-of-the-service"></a>서비스의 상태에 대한 메시지  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치하도록 선택하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 설치되고 시작되며, 시작 유형은 자동으로 설정됩니다.  
  
|이벤트 ID|심볼 이름|텍스트|메모|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스를 시작하고 있습니다.|서비스를 시작하려고 합니다.|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스가 시작되었습니다.|서비스가 시작되었습니다.|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스를 시작하지 못했습니다.%n오류: %1|서비스를 시작하지 못했습니다. 서비스를 시작할 수 없는 것은 손상된 설치 또는 부적절한 서비스 계정 때문일 수 있습니다.|  
|258|DTS_MSG_SERVER_STOPPING|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스를 중지하고 있습니다.%n%n종료 시 실행 중인 모든 패키지를 중지합니다. %1|서비스가 중지될 때 해당 서비스가 실행 중인 모든 패키지를 중지하도록 구성한 경우 실행 중인 패키지가 모두 중지됩니다. 구성 파일에서 서비스 자체가 중지될 때 해당 서비스가 실행 중인 패키지를 중지할지 여부를 결정하는 true 또는 false 값을 설정할 수 있습니다. 이 이벤트 메시지에는 이러한 설정에 대한 값이 포함되어 있습니다.|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스가 중지되었습니다.%n서버 버전 %1|서비스가 중지되었습니다.|  
  
## <a name="messages-about-the-configuration-file"></a>구성 파일에 대한 메시지  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 설정은 수정 가능한 XML 파일에 저장됩니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../configuring-the-integration-services-service-ssis-service.md)버전과의 호환성을 위한 서비스를 지원합니다.  
  
|이벤트 ID|심볼 이름|텍스트|메모|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스: %n구성 파일을 지정하는 레지스트리 설정이 없습니다. %n기본 구성 파일을 로드하려고 합니다.|구성 파일의 경로가 포함된 레지스트리 항목이 없거나 비어 있습니다.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스 구성 파일이 없습니다.%n기본 설정을 사용하여 로드하고 있습니다.|지정된 위치에 구성 파일 자체가 없습니다.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스 구성 파일이 잘못되었습니다.%n구성 파일을 읽는 중 오류가 발생했습니다. %1%n%n기본 설정을 사용하여 서버를 로드합니다.|구성 파일을 로드할 수 없거나 구성 파일이 유효하지 않습니다. 이 오류는 구성 파일의 XML 구문 오류 때문에 발생할 수 있습니다.|  
  
## <a name="other-messages"></a>기타 메시지  
  
|이벤트 ID|심볼 이름|텍스트|메모|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스: 패키지 실행을 중지하고 있습니다.%n패키지 인스턴스 ID: %1%n패키지 ID: %2%n패키지 이름: %3%n패키지 설명: %4%n패키지|서비스가 실행 중인 패키지를 중지하려고 하고 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 실행 중인 패키지를 모니터링하고 중지할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 패키지를 관리하는 방법은 [패키지 관리&#40;SSIS 서비스&#41;](package-management-ssis-service.md)를 참조하세요.|  
  
## <a name="related-tasks"></a>관련 작업  
 로그 항목을 보는 방법은 [이벤트 로그 창에서 로그 항목 보기](../view-log-entries-in-the-log-events-window.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [통합 서비스 패키지에 의해 기록된 이벤트](../performance/events-logged-by-an-integration-services-package.md)  
  
  
