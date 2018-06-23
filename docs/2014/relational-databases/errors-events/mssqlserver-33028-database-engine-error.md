---
title: MSSQLSERVER_33028 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ccf8eeb5d9c91e1f8ec8cec3c46edf66409bbc5a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080635"
---
# <a name="mssqlserver33028"></a>MSSQLSERVER_33028
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|33028|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_CRYPTOPROV_CANTOPENSESSION|  
|메시지 텍스트|%S_MSG '%.*ls'에 대한 세션을 열 수 없습니다. 공급자 오류 코드: %d.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 위의 오류 메시지에 나열된 암호화 공급자를 열 수 없습니다. 암호화 공급자가 위의 오류 코드를 제공했습니다. 암호화 공급자에게 오류에 대한 자세한 정보를 문의해야 할 수 있습니다.  
  
|오류 코드|Description|  
|----------------|-----------------|  
|0|성공했습니다. 오류가 없습니다.|  
|1|실패. 지정되지 않았거나 예기치 않은 오류가 발생했습니다. 사용할 수 있는 추가 정보가 없습니다.|  
|2|부족한 버퍼. 암호화 공급자가 사용할 공간을 할당할 수 없습니다.|  
|3|지원되지 않음. 암호화 공급자가 이 릴리스에서 지원되지 않습니다. 다른 암호화 공급자를 선택하십시오.|  
|4|찾을 수 없음. 지정된 암호화 공급자가 없거나 해당 파일에 액세스할 수 있는 권한을 가지고 있지 않습니다.|  
|5|권한 부여 실패. 자격 증명을 만들 때 잘못된 암호나 사용자 이름을 제공할 경우 발생할 수 있습니다. 또한 자격 증명이 없는 경우에도 발생할 수 있습니다.|  
|6|인수가 잘못되었습니다. 암호화 공급자에게 잘못된 인수가 전달되었습니다.|  
  
## <a name="user-action"></a>사용자 동작  
 오류를 해결하거나 암호화 공급자에게 자세한 정보를 문의합니다.  
  
  