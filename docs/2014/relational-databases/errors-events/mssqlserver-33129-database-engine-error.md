---
title: MSSQLSERVER_33129 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b879bcb492783eec2cbca121f2596d096e2f673f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184282"
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|33129|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_CANNOT_DISABLE_WIN_GROUP|  
|메시지 텍스트|ALTER_LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 이 메시지는 Windows 그룹의 로그인을 사용하지 않도록 설정할 때 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 Windows 그룹의 로그인은 사용하지 않도록 설정할 수 없습니다. Windows 그룹에 부여된 액세스 권한을 임시로 제거하려면 Windows 그룹의 로그인에 대한 CONNECT 권한을 취소합니다. 그래도 Windows 사용자는 자신의 개별 로그인이나 다른 Windows 그룹을 통해 액세스할 수 있습니다. 다음 예에서는 WESTCOAST 도메인의 Accounting 그룹에 대한 연결 권한을 취소합니다.  
  
```tsql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  