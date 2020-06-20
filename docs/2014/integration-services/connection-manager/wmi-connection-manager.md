---
title: WMI 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29ddc30f89621e9b4875a57c191a81ef3f10784d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920274"
---
# <a name="wmi-connection-manager"></a>WMI 연결 관리자
  WMI 연결 관리자를 사용하면 패키지에서 WMI(Windows Management Instrumentation)를 사용하여 엔터프라이즈 환경의 정보를 관리할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 웹 서비스 태스크에서는 WMI 연결 관리자가 사용됩니다.  
  
 패키지에 WMI 연결 관리자를 추가 하면에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 wmi 연결로 확인 되는 연결 관리자를 만들고, 연결 관리자 속성을 설정 하 고, 연결 관리자를 `Connections` 패키지의 컬렉션에 추가 합니다. 연결 관리자의 `ConnectionManagerType` 속성이 `WMI`로 설정됩니다.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>WMI 연결 관리자 구성  
 다음과 같은 방법으로 WMI 연결 관리자를 구성할 수 있습니다.  
  
-   서버의 이름을 지정합니다.  
  
-   서버에 네임스페이스를 지정합니다.  
  
-   서버에 연결하기 위한 인증 모드를 선택합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [WMI 연결 관리자 편집기](../wmi-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스 태스크](../control-flow/web-service-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
