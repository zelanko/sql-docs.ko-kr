---
description: MSSQLSERVER_26014
title: MSSQLSERVER_26014 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9bb0b7deb6927cf319083a63c789fc1fbf07a26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424465"
---
# <a name="mssqlserver_26014"></a>MSSQLSERVER_26014
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
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
  
