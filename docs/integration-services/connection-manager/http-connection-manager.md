---
title: "HTTP 연결 관리자 | Microsoft Docs"
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
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9efb5b8d8a972cfc60ccb078363bcba055eea01
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="http-connection-manager"></a>HTTP 연결 관리자
  HTTP 연결을 사용하면 패키지에서 HTTP를 통해 웹 서버에 액세스하고 파일을 보내거나 받을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 웹 서비스 태스크에서는 이 연결 관리자가 사용됩니다.  
  
 패키지에 HTTP 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 HTTP 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **HTTP.**로 설정됩니다.  
  
 다음과 같은 방법으로 HTTP 연결 관리자를 구성할 수 있습니다.  
  
-   자격 증명을 사용합니다. 연결 관리자에서 자격 증명이 사용되는 경우 해당 속성에는 사용자 이름, 암호 및 도메인이 포함됩니다.  
  
    > [!IMPORTANT]  
    >  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
-   클라이언트 인증서를 사용합니다. 연결 관리자에서 클라이언트 인증서가 사용되는 경우 해당 속성에는 인증서 이름이 포함됩니다.  
  
-   서버 연결에 대한 제한 시간 값과 데이터 기록에 대한 청크 크기를 제공합니다.  
  
-   프록시 서버를 사용합니다. 자격 증명을 사용하고 프록시 서버 대신 로컬 주소를 사용하도록 프록시 서버를 구성할 수도 있습니다.  
  
## <a name="configuration-of-the-http-connection-manager"></a>HTTP 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>를 참조하세요.  
  
## <a name="http-connection-manager-editor-server-page"></a>HTTP 연결 관리자 편집기(서버 페이지)
  **HTTP 연결 관리자 편집기** 대화 상자의 **서버** 탭에서 URL이나 보안 자격 증명 등의 속성을 지정하여 HTTP 연결 관리자를 구성할 수 있습니다. HTTP 연결을 사용하면 패키지에서 HTTP를 통해 웹 서버에 액세스하고 파일을 보내거나 받을 수 있습니다. HTTP 연결 관리자를 구성했으면 연결을 테스트할 수도 있습니다.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 HTTP 연결 관리자에 대한 자세한 내용은 [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)를 참조하십시오. HTTP 연결 관리자의 일반적인 사용 시나리오에 대한 자세한 내용은 [Web Service Task](../../integration-services/control-flow/web-service-task.md)를 참조하십시오.  
  
### <a name="options"></a>변수  
 **서버 URL**  
 서버의 URL을 입력합니다.  
  
 **웹 서비스 태스크 편집기** 의 **일반** 페이지에 있는 **WSDL 다운로드** 단추를 사용하여 WSDL 파일을 다운로드하려면 WSDL 파일의 URL을 입력합니다. 이 URL은 "?wsdl"로 끝납니다.  
  
 **자격 증명 사용**  
 HTTP 연결 관리자에서 사용자의 보안 자격 증명을 인증에 사용할지 여부를 지정합니다.  
  
 **User name**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **암호**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **도메인**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **클라이언트 인증서 사용**  
 HTTP 연결 관리자에서 클라이언트 인증서를 인증에 사용할지 여부를 지정합니다.  
  
 **인증서**  
 **인증서 선택** 대화 상자를 사용하여 목록에서 인증서를 선택합니다. 입력란에 해당 인증서와 연결된 이름이 표시됩니다.  
  
 **제한 시간(초)**  
 웹 서버에 연결하기 위한 제한 시간을 제공합니다. 이 속성의 기본값은 30초입니다.  
  
 **청크 크기(KB)**  
 데이터를 쓰기 위한 청크 크기를 제공합니다.  
  
 **연결 테스트**  
 HTTP 연결 관리자를 구성했으면 **연결 테스트**를 클릭하여 연결이 실행 가능한지 확인합니다.  
  
## <a name="http-connection-manager-editor-proxy-page"></a>HTTP 연결 관리자 편집기(프록시 페이지)
  **HTTP 연결 관리자 편집기** 대화 상자의 **프록시** 탭을 사용하여 프록시 서버를 사용하도록 HTTP 연결 관리자를 구성할 수 있습니다. HTTP 연결을 사용하면 패키지에서 HTTP를 통해 웹 서버에 액세스하고 파일을 보내거나 받을 수 있습니다.  
  
 HTTP 연결 관리자에 대한 자세한 내용은 [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)를 참조하십시오. HTTP 연결 관리자의 일반적인 사용 시나리오에 대한 자세한 내용은 [Web Service Task](../../integration-services/control-flow/web-service-task.md)를 참조하십시오.  
  
### <a name="options"></a>변수  
 **프록시 사용**  
 HTTP 연결 관리자에서 프록시 서버를 통해 연결하도록 할지 여부를 지정합니다.  
  
 **프록시 URL**  
 프록시 서버의 URL을 입력합니다.  
  
 **로컬에서 프록시 사용 안 함**  
 HTTP 연결 관리자에서 로컬 주소에 대해 프록시 서버를 사용하지 않도록 할지 여부를 지정합니다.  
  
 **자격 증명 사용**  
 HTTP 연결 관리자에서 프록시 서버에 보안 자격 증명을 사용하도록 할지 여부를 지정합니다.  
  
 **User name**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **암호**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **도메인**  
 HTTP 연결 관리자에서 자격 증명을 사용하는 경우에는 사용자 이름, 암호 및 도메인을 지정해야 합니다.  
  
 **프록시 무시 목록**  
 프록시 서버를 사용하지 않도록 지정할 주소 목록입니다.  
  
 **추가**  
 프록시 서버를 사용하지 않도록 할 주소를 입력합니다.  
  
 **제거**  
 주소를 선택한 다음 **제거**를 클릭하여 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스 태스크](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
