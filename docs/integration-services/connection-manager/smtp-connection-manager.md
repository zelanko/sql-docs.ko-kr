---
title: SMTP 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa08bc78b491fd33c3f904b03caed2f4466512e5
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728127"
---
# <a name="smtp-connection-manager"></a>SMTP 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SMTP 연결 관리자를 사용하면 패키지에서 SMTP(Simple Mail Transfer Protocol) 서버에 연결할 수 있습니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 메일 보내기 태스크에서는 SMTP 연결 관리자가 사용됩니다.  
  
 Microsoft Exchange를 SMTP 서버로 사용하는 경우 Windows 인증을 사용하려면 SMTP 연결 관리자를 구성해야 할 수 있습니다. 인증되지 않은 SMTP 연결을 허용하지 않도록 Exchange 서버를 구성할 수도 있습니다.  
  
## <a name="configuration-the-smtp-connection-manager"></a>SMTP 연결 관리자 구성  
 패키지에 SMTP 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 SMTP 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 연결 관리자의 **ConnectionManagerType** 속성이 **SMTP**로 설정됩니다.  
  
 다음과 같은 방법으로 SMTP 연결 관리자를 구성할 수 있습니다.  
  
-   연결 문자열을 제공합니다.  
  
-   SMTP 서버의 이름을 지정합니다.  
  
-   사용할 인증 방법을 지정합니다.  
  
    > [!IMPORTANT]  
    >  SMTP 연결 관리자는 익명 인증과 Windows 인증만 지원하며 기본 인증은 지원하지 않습니다.  
  
-   전자 메일 메시지를 보낼 때 SSL(Secure Sockets Layer)을 사용하여 통신을 암호화할지 여부를 지정합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [SMTP 연결 관리자 편집기](../../integration-services/connection-manager/smtp-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="smtp-connection-manager-editor"></a>SMTP 연결 관리자 편집기
  **SMTP 연결 관리자 편집기** 대화 상자를 사용하여 SMTP(Simple Mail Transfer Protocol) 서버를 지정할 수 있습니다.  
  
 SMTP 연결 관리자에 대한 자세한 내용은 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **이름**  
 연결 관리자의 고유 이름을 제공합니다.  
  
 **설명**  
 연결 관리자에 대한 설명을 입력합니다. 설명에 해당 연결 관리자의 용도를 정의하면 패키지를 이해하기 쉬우며 유지 관리가 간편합니다.  
  
 **SMTP 서버**  
 SMTP 서버의 이름을 제공합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 통해 서버에 대한 액세스를 인증하는 SMTP 서버를 사용하여 메일을 보내려면 선택합니다.  
  
> [!IMPORTANT]  
>  SMTP 연결 관리자는 익명 인증과 Windows 인증만 지원하며 기본 인증은 지원하지 않습니다.  
  
> [!NOTE]  
>  Microsoft Exchange를 SMTP 서버로 사용하는 경우 **Windows 인증 사용** 을 **True**로 설정해야 할 수 있습니다. 인증되지 않은 SMTP 연결을 허용하지 않도록 Exchange Server를 구성할 수도 있습니다.  
  
 **SSL(Secure Sockets Layer) 사용**  
 전자 메일 메시지를 보낼 때 SSL(Secure Sockets Layer)을 사용하여 통신을 암호화하려면 선택합니다.  
  
