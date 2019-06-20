---
title: HTTP 연결 관리자 편집기 (서버 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 197a2668beb60acf2473a1f53786d7b553e08cf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058251"
---
# <a name="http-connection-manager-editor-server-page"></a>HTTP 연결 관리자 편집기(서버 페이지)
  **HTTP 연결 관리자 편집기** 대화 상자의 **서버** 탭에서 URL이나 보안 자격 증명 등의 속성을 지정하여 HTTP 연결 관리자를 구성할 수 있습니다. HTTP 연결을 사용하면 패키지에서 HTTP를 통해 웹 서버에 액세스하고 파일을 보내거나 받을 수 있습니다. HTTP 연결 관리자를 구성했으면 연결을 테스트할 수도 있습니다.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 HTTP 연결 관리자에 대한 자세한 내용은 [HTTP Connection Manager](connection-manager/http-connection-manager.md)를 참조하십시오. HTTP 연결 관리자의 일반적인 사용 시나리오에 대한 자세한 내용은 [Web Service Task](control-flow/web-service-task.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **서버 URL**  
 서버의 URL을 입력합니다.  
  
 **웹 서비스 태스크 편집기** 의 **일반** 페이지에 있는 **WSDL 다운로드** 단추를 사용하여 WSDL 파일을 다운로드하려면 WSDL 파일의 URL을 입력합니다. 이 URL은 "?wsdl"로 끝납니다.  
  
 **자격 증명 사용**  
 HTTP 연결 관리자에서 사용자의 보안 자격 증명을 인증에 사용할지 여부를 지정합니다.  
  
 **사용자 이름**  
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
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [HTTP 연결 관리자 편집기&#40;프록시 페이지&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
