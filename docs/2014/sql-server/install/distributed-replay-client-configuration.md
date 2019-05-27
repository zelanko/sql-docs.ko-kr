---
title: Distributed Replay Client 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3eb00922b4f6e21dd4cfc8a46d8c0c27ed9a5be1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095482"
---
# <a name="distributed-replay-client-configuration"></a>Distributed Replay Client 구성
  **설치 마법사의** Distributed Replay Client 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 Distributed Replay Client 서비스에 대한 관리 권한을 부여할 사용자를 지정합니다.  
  
 관리 권한이 있는 사용자는 Distributed Replay Client 서비스에 무제한으로 액세스할 수 있습니다.  
  
## <a name="options"></a>변수  
 **컨트롤러 이름**  
 이 선택적 매개 변수 이며 기본값은 \< *빈*>.  
  
 클라이언트 컴퓨터에서 Distributed Replay Client 서비스를 위해 통신할 컨트롤러의 이름을 입력합니다. 다음에 유의하세요.  
  
-   이는 FQDN(정규화된 도메인 이름)이어야 합니다. 예를 들어, Microsoft의 제품 계층에서 server1이라는 호스트의 FQDN은 server1.products.microsoft.com일 수 있습니다.  
  
-   컨트롤러를 이미 설정한 경우 각 클라이언트를 구성할 때 컨트롤러의 이름을 입력합니다.  
  
-   컨트롤러를 아직 설정하지 않은 경우에는 컨트롤러 이름을 비워 둡니다. 그러나 **클라이언트 구성** 파일에서 컨트롤러 이름을 수동으로 입력해야 합니다.  
  
 **작업 디렉터리**  
 Distributed Replay Client 서비스의 작업 디렉터리를 지정합니다.  
  
 기본 작업 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\입니다.  
  
 **결과 디렉터리**  
 Distributed Replay Client 서비스의 결과 디렉터리를 지정합니다.  
  
 기본 결과 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\입니다.  
  
  
