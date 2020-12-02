---
description: FTP 연결 관리자
title: FTP 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 854f975c64f5622c53d04c51651929d83745864a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91728048"
---
# <a name="ftp-connection-manager"></a>FTP 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  FTP 연결 관리자를 사용하면 패키지에서 FTP(파일 전송 프로토콜) 서버에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 FTP 태스크에서는 이 연결 관리자가 사용됩니다.  
  
 패키지에 FTP 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 FTP 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **FTP** 로 설정됩니다.  
  
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
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [FTP 연결 관리자 편집기]()를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="ftp-connection-manager-editor"></a>FTP 연결 관리자 편집기
  **FTP 연결 관리자 편집기** 대화 상자를 사용하여 FTP 서버 연결 속성을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  FTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 FTP 연결 관리자에 대한 자세한 내용은 [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **서버 이름**  
 FTP 서버의 이름을 제공합니다.  
  
 **서버 포트**  
 연결에 사용할 FTP 서버의 포트 번호를 지정합니다. 이 속성의 기본값은 **21** 입니다.  
  
 **사용자 이름**  
 FTP 서버에 액세스하기 위한 사용자 이름을 제공합니다. 이 속성의 기본값은 **anonymous** 입니다.  
  
 **암호**  
 FTP 서버에 액세스하기 위한 암호를 제공합니다.  
  
 **제한 시간(초)**  
 태스크가 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 값 **0** 은 시간 제한이 없음을 의미합니다. 이 속성의 기본값은 **60** 입니다.  
  
 **Passive 모드 사용**  
 서버가 연결을 시작하는지 또는 클라이언트가 연결을 시작하는지 지정합니다. 서버는 Active 모드로 연결을 시작하고 클라이언트는 Passive 모드로 연결을 활성화합니다. 이 속성의 기본값은 **active mode** 입니다.  
  
 **재시도**  
 태스크가 연결하려고 하는 횟수를 지정합니다. 값 **0** 은 시도 횟수에 제한이 없다는 것을 나타냅니다.  
  
 **청크 크기(KB)**  
 데이터를 전송하기 위한 청크 크기(KB)를 제공합니다.  
  
 **연결 테스트**  
 FTP 연결 관리자를 구성했으면 **연결 테스트** 를 클릭하여 연결이 실행 가능한지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [FTP 태스크](../../integration-services/control-flow/ftp-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
