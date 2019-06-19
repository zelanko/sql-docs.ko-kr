---
title: FTP 연결 관리자 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP Connection Manager Editor
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 090b4d990a516b412ae5f7cc4e4d6e766e8d02e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058484"
---
# <a name="ftp-connection-manager-editor"></a>FTP 연결 관리자 편집기
  **FTP 연결 관리자 편집기** 대화 상자를 사용하여 FTP 서버 연결 속성을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  FTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 FTP 연결 관리자에 대한 자세한 내용은 [FTP Connection Manager](connection-manager/ftp-connection-manager.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **서버 이름**  
 FTP 서버의 이름을 제공합니다.  
  
 **서버 포트**  
 연결에 사용할 FTP 서버의 포트 번호를 지정합니다. 이 속성의 기본값은 **21**입니다.  
  
 **사용자 이름**  
 FTP 서버에 액세스하기 위한 사용자 이름을 제공합니다. 이 속성의 기본값은 **anonymous**입니다.  
  
 **암호**  
 FTP 서버에 액세스하기 위한 암호를 제공합니다.  
  
 **제한 시간(초)**  
 태스크가 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 값 **0** 은 시간 제한이 없음을 의미합니다. 이 속성의 기본값은 **60**입니다.  
  
 **Passive 모드 사용**  
 서버가 연결을 시작하는지 또는 클라이언트가 연결을 시작하는지 지정합니다. 서버는 Active 모드로 연결을 시작하고 클라이언트는 Passive 모드로 연결을 활성화합니다. 이 속성의 기본값은 **active mode**입니다.  
  
 **다시 시도**  
 태스크가 연결하려고 하는 횟수를 지정합니다. 값 **0** 은 시도 횟수에 제한이 없다는 것을 나타냅니다.  
  
 **청크 크기(KB)**  
 데이터를 전송하기 위한 청크 크기(KB)를 제공합니다.  
  
 **연결 테스트**  
 FTP 연결 관리자를 구성했으면 **연결 테스트**를 클릭하여 연결이 실행 가능한지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
