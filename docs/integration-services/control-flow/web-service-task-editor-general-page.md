---
title: "웹 서비스 태스크 편집기(일반 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.webservicestask.general.f1"
helpviewer_keywords: 
  - "웹 서비스 태스크 편집기"
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# 웹 서비스 태스크 편집기(일반 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 HTTP 연결 관리자를 지정하고, 웹 서비스 태스크에 사용하는 WSDL(웹 서비스 기술 언어) 파일의 위치를 지정하고, 웹 서비스 태스크를 설명하고, WSDL 파일을 다운로드할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [웹 서비스 태스크](../../integration-services/control-flow/web-service-task.md)를 참조하세요.  
  
## 옵션  
 **HTTPConnection**  
 목록에서 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 **관련 항목:** [HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md), [HTTP 연결 관리자 편집기&#40;서버 페이지&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 컴퓨터에 로컬인 WSDL 파일의 정규화된 경로를 입력하거나 찾아보기 단추**(…)**를 클릭하여 이 파일을 찾습니다.  
  
 WSDL 파일을 컴퓨터에 이미 수동으로 다운로드한 경우에는 이 파일을 선택하고, WSDL 파일을 아직 다운로드하지 않은 경우에는 다음 단계를 수행합니다.  
  
-   파일 이름 확장명이 ".wsdl"인 빈 파일을 만듭니다.  
  
-   **WSDLFile** 옵션으로 이 빈 파일을 선택합니다.  
  
-   **OverwriteWSDLFile** 값을 **True** 로 설정하여 이 빈 파일을 실제 WSDL 파일로 덮어쓸 수 있도록 합니다.  
  
-   **WSDL 다운로드** 를 클릭하여 실제 WSDL 파일을 다운로드하고 빈 파일을 덮어씁니다.  
  
    > [!NOTE]  
    >  **WSDL 다운로드** 옵션은 **WSDLFile** 상자에 기존 로컬 파일의 이름을 입력할 때까지 사용할 수 없습니다.  
  
 **OverwriteWSDLFile**  
 웹 서비스 태스크에 대한 WSDL 파일을 덮어쓸지 여부를 나타냅니다.  
  
 **WSDL 다운로드** 단추를 사용하여 WSDL 파일을 다운로드하려면 이 값을 **True**로 설정합니다.  
  
 **이름**  
 웹 서비스 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **Description**  
 웹 서비스 태스크에 대한 설명을 입력합니다.  
  
 **WSDL 다운로드**  
 WSDL 파일을 다운로드합니다.  
  
 이 단추는 **WSDLFile** 상자에 기존 로컬 파일의 이름을 입력할 때까지 사용할 수 없습니다.  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [웹 서비스 태스크 편집기&#40;입력 페이지&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [웹 서비스 태스크 편집기&#40;출력 페이지&#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
  