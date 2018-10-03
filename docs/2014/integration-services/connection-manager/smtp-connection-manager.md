---
title: SMTP 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a5ede293cf4965d89e333d1672a15de6811ec8d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084953"
---
# <a name="smtp-connection-manager"></a>SMTP 연결 관리자
  SMTP 연결 관리자를 사용하면 패키지에서 SMTP(Simple Mail Transfer Protocol) 서버에 연결할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 메일 보내기 태스크에서는 SMTP 연결 관리자가 사용됩니다.  
  
 Microsoft Exchange를 SMTP 서버로 사용하는 경우 Windows 인증을 사용하려면 SMTP 연결 관리자를 구성해야 할 수 있습니다. 인증되지 않은 SMTP 연결을 허용하지 않도록 Exchange 서버를 구성할 수도 있습니다.  
  
## <a name="configuration-the-smtp-connection-manager"></a>SMTP 연결 관리자 구성  
 패키지에 SMTP 연결 관리자를 추가 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결한 런타임에 SMTP 연결으로 확인 되는 연결 관리자 속성을 설정 하 고 연결 관리자를 추가 하는 관리자는 `Connections` 컬렉션에는 패키지입니다. 합니다 `ConnectionManagerType` 연결 관리자의 속성이 `SMTP`합니다.  
  
 다음과 같은 방법으로 SMTP 연결 관리자를 구성할 수 있습니다.  
  
-   연결 문자열을 제공합니다.  
  
-   SMTP 서버의 이름을 지정합니다.  
  
-   사용할 인증 방법을 지정합니다.  
  
    > [!IMPORTANT]  
    >  SMTP 연결 관리자는 익명 인증과 Windows 인증만 지원하며 기본 인증은 지원하지 않습니다.  
  
-   전자 메일 메시지를 보낼 때 SSL(Secure Sockets Layer)을 사용하여 통신을 암호화할지 여부를 지정합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [SMTP 연결 관리자 편집기](../smtp-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 하 고 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
  
