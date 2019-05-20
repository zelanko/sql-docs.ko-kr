---
title: SMO 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03373dc9714d992c36ca29611013979d1c62ecf6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728125"
---
# <a name="smo-connection-manager"></a>SMO 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SMO 연결 관리자를 사용하면 패키지에서 SMO(SQL Management Objects) 서버에 연결할 수 있습니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 전송 태스크에서는 SMO 연결 관리자가 사용됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 전송하는 전송 로그인 태스크에서는 SMO 연결 관리자가 사용됩니다.  
  
 패키지에 SMO 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 SMO 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 연결 관리자의 **ConnectionManagerType** 속성이 **SMOServer**로 설정됩니다.  
  
 다음과 같은 방법으로 SMO 연결 관리자를 구성할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 서버의 이름을 지정합니다.  
  
-   서버에 연결하기 위한 인증 모드를 선택합니다.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>SMO 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [SMO 연결 관리자 편집기](../../integration-services/connection-manager/smo-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="smo-connection-manager-editor"></a>SMO 연결 관리자 편집기
  **SMO 연결 관리자 편집기** 를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 전송하는 여러 태스크에 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 구성할 수 있습니다.  
  
 SMO 연결 관리자에 대한 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **서버 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력하거나 목록에서 서버 이름을 선택합니다.  
  
 **새로 고침**  
 네트워크에서 검색할 수 있는 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 목록을 새로 고칩니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
 **User name**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 암호를 입력합니다.  
  
 **연결 테스트**  
 구성한 연결을 테스트합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
