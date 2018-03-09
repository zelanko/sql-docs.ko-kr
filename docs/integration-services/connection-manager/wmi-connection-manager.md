---
title: "WMI 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d432432905afd9a1ef2355e16540cc5caa64e0a2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="wmi-connection-manager"></a>WMI 연결 관리자
  WMI 연결 관리자를 사용하면 패키지에서 WMI(Windows Management Instrumentation)를 사용하여 엔터프라이즈 환경의 정보를 관리할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함되는 웹 서비스 태스크에서는 WMI 연결 관리자가 사용됩니다.  
  
 패키지에 WMI 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 WMI 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 연결 관리자의 **ConnectionManagerType** 속성이 **WMI**로 설정됩니다.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>WMI 연결 관리자 구성  
 다음과 같은 방법으로 WMI 연결 관리자를 구성할 수 있습니다.  
  
-   서버의 이름을 지정합니다.  
  
-   서버에 네임스페이스를 지정합니다.  
  
-   서버에 연결하기 위한 인증 모드를 선택합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [WMI 연결 관리자 편집기](../../integration-services/connection-manager/wmi-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="wmi-connection-manager-editor"></a>WMI 연결 관리자 편집기
  **WMI 연결 관리자** 대화 상자를 사용하여 서버에 대한 Microsoft WMI(Windows Management Instrumentation) 연결을 지정할 수 있습니다.  
  
 WMI 연결 관리자에 대한 자세한 내용은 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>변수  
 **이름**  
 연결 관리자의 고유 이름을 제공합니다.  
  
 **설명**  
 연결 관리자에 대한 설명을 입력합니다. 설명에 해당 연결 관리자의 용도를 정의하면 패키지를 이해하기 쉬우며 유지 관리가 간편합니다.  
  
 **서버 이름**  
 WMI 연결을 만들 서버의 이름을 제공합니다.  
  
 **Namespace**  
 WMI 네임스페이스를 지정합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하려면 선택합니다. Windows 인증을 사용하면 연결할 때 사용자 이름 또는 암호를 제공할 필요가 없습니다.  
  
 **User name**  
 Windows 인증을 사용하지 않으면 연결할 때 사용자 이름을 제공해야 합니다.  
  
 **암호**  
 Windows 인증을 사용하지 않으면 연결할 때 암호를 제공해야 합니다.  
  
 **테스트**  
 연결 관리자 설정을 테스트합니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스 태스크](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
