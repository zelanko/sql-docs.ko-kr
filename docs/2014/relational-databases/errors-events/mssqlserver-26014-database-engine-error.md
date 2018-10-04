---
title: MSSQLSERVER_26014 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edebfb36a1693f2a7d6a94d7c006d80e2bb27683
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151573"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|26014|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SNI_SSL_USER_CERT_FAILURE|  
|메시지 텍스트|사용자 지정 인증서 [인증서 해시(sha1) "%hs"]을(를) 로드할 수 없습니다. 서버가 연결을 허용하지 않습니다. 인증서가 제대로 설치되어 있는지 확인해야 합니다. 온라인 설명서에서 "SSL에 사용되는 인증서 구성"을 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메시지에 명명된 인증서를 로드하려고 시도했지만 실패했습니다. 이 문제를 해결해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 인증서를 사용할 수 있습니다.  
  
 가능한 원인은 다음과 같습니다.  
  
-   인증서가 이동되었거나 삭제되었습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 로그인이 변경된 경우 인증서에 액세스하는 데 필요한 사용 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 없을 수 있습니다.  
  
-   인증서가 만료되었을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 메시지에 명명된 인증서가 시스템에 있는지, 액세스 가능한지, 사용할 수 있는지 확인하십시오.  
  
  
