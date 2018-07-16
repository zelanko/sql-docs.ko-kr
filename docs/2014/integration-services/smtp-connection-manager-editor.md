---
title: SMTP 연결 관리자 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
caps.latest.revision: 37
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c67233452d294a6bc0f6f106a59678827ef17b3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235213"
---
# <a name="smtp-connection-manager-editor"></a>SMTP 연결 관리자 편집기
  **SMTP 연결 관리자 편집기** 대화 상자를 사용하여 SMTP(Simple Mail Transfer Protocol) 서버를 지정할 수 있습니다.  
  
 SMTP 연결 관리자에 대한 자세한 내용은 [SMTP Connection Manager](connection-manager/smtp-connection-manager.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
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
>  Microsoft Exchange를 SMTP 서버로 사용으로 설정 해야 하면 **Windows 인증 사용** 에 `True`입니다. 인증되지 않은 SMTP 연결을 허용하지 않도록 Exchange Server를 구성할 수도 있습니다.  
  
 **SSL(Secure Sockets Layer) 사용**  
 전자 메일 메시지를 보낼 때 SSL(Secure Sockets Layer)을 사용하여 통신을 암호화하려면 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
