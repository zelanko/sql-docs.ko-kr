---
title: FTP 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 02501b845254301a8370fcd208d849a6c6e3e3a9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920856"
---
# <a name="ftp-connection-manager"></a>FTP 연결 관리자
  FTP 연결 관리자를 사용하면 패키지에서 FTP(파일 전송 프로토콜) 서버에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 FTP 태스크에서는 이 연결 관리자가 사용됩니다.  
  
 패키지에 FTP 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 런타임에 FTP 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 `Connections` 컬렉션에 추가합니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `FTP`로 설정됩니다.  
  
 다음과 같은 방법으로 FTP 연결 관리자를 구성할 수 있습니다.  
  
-   서버 이름과 서버 포트를 지정합니다.  
  
-   익명 액세스를 지정하거나 기본 인증을 위한 사용자 이름과 암호를 제공합니다.  
  
    > [!IMPORTANT]  
    >  FTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
-   제한 시간, 다시 시도 횟수 및 한 번에 복사할 데이터 양을 설정합니다.  
  
-   FTP 연결 관리자에서 Passive 또는 Active 모드를 사용할지 여부를 나타냅니다.  
  
 FTP 연결 관리자에서 연결하는 FTP 사이트의 구성에 따라 연결 관리자의 다음 기본값을 변경해야 합니다.  
  
-   서버 포트는 21로 설정됩니다. FTP사이트에서 수신하는 포트를 지정해야 합니다.  
  
-   사용자 이름은 "anonymous"로 설정됩니다. FTP 사이트에 필요한 자격 증명을 제공해야 합니다.  
  
## <a name="activepassive-modes"></a>Active/Passive 모드  
 FTP 연결 관리자는 Active 모드 또는 Passive 모드를 사용하여 파일을 보내고 받을 수 있습니다. Active 모드에서는 서버가 데이터 연결을 시작하고, Passive 모드에서는 클라이언트가 데이터 연결을 시작합니다.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>FTP 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [FTP 연결 관리자 편집기](../ftp-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [FTP 태스크](../control-flow/ftp-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
