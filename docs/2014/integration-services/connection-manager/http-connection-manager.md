---
title: HTTP 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f79a882e3a3e4520cb8cfcd4468f3c908b79abf5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833761"
---
# <a name="http-connection-manager"></a>HTTP 연결 관리자
  HTTP 연결을 사용하면 패키지에서 HTTP를 통해 웹 서버에 액세스하고 파일을 보내거나 받을 수 있습니다. 에서 포함 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 웹 서비스 태스크는이 연결 관리자를 사용 합니다.  
  
 패키지에 HTTP 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 런타임에 HTTP 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하며, 연결 관리자를 패키지의 `Connections` 컬렉션에 추가합니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `HTTP.`로 설정됩니다.  
  
 다음과 같은 방법으로 HTTP 연결 관리자를 구성할 수 있습니다.  
  
-   자격 증명을 사용합니다. 연결 관리자에서 자격 증명이 사용되는 경우 해당 속성에는 사용자 이름, 암호 및 도메인이 포함됩니다.  
  
    > [!IMPORTANT]  
    >  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
-   클라이언트 인증서를 사용합니다. 연결 관리자에서 클라이언트 인증서가 사용되는 경우 해당 속성에는 인증서 이름이 포함됩니다.  
  
-   서버 연결에 대한 제한 시간 값과 데이터 기록에 대한 청크 크기를 제공합니다.  
  
-   프록시 서버를 사용합니다. 자격 증명을 사용하고 프록시 서버 대신 로컬 주소를 사용하도록 프록시 서버를 구성할 수도 있습니다.  
  
## <a name="configuration-of-the-http-connection-manager"></a>HTTP 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [HTTP 연결 관리자 편집기 &#40;서버 페이지&#41;](../http-connection-manager-editor-server-page.md)  
  
-   [HTTP 연결 관리자 편집기 &#40;프록시 페이지&#41;](../http-connection-manager-editor-proxy-page.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스 태스크](../control-flow/web-service-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
