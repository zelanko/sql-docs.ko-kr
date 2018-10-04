---
title: SMO 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a095e6c0e7204bd74892156af4ddc05f3f383eb0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201068"
---
# <a name="smo-connection-manager"></a>SMO 연결 관리자
  SMO 연결 관리자를 사용하면 패키지에서 SMO(SQL Management Objects) 서버에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 전송 태스크에서는 SMO 연결 관리자가 사용됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 전송하는 전송 로그인 태스크에서는 SMO 연결 관리자가 사용됩니다.  
  
 패키지에 SMO 연결 관리자를 추가 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결한 런타임에 SMO 연결으로 확인 되는 연결 관리자 속성을 설정 하 고 연결 관리자를 추가 하는 관리자는 `Connections` 컬렉션에는 패키지입니다. 합니다 `ConnectionManagerType` 연결 관리자의 속성이 `SMOServer`합니다.  
  
 다음과 같은 방법으로 SMO 연결 관리자를 구성할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 서버의 이름을 지정합니다.  
  
-   서버에 연결하기 위한 인증 모드를 선택합니다.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>SMO 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [SMO 연결 관리자 편집기](../smo-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 하 고 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
