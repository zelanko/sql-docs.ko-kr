---
title: MSSQLSERVER_102 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a37d88aba148cd93e77b21254f9451ad22b32225
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419962"
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|102|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|P_SYNTAXERR2|  
|메시지 텍스트|'%.*ls' 근처의 구문이 잘못되었습니다.|  
  
## <a name="explanation"></a>설명  
 구문 오류를 나타냅니다. 오류로 인해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 문을 처리할 수 없기 때문에 추가 정보를 확인할 수 없습니다.  
  
 이 오류는 90 또는 100 호환성 모드가 아닐 경우 사용되지 않는 RC4 또는 RC4_128 암호화를 사용하여 대칭 키를 만들려고 할 때 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 구문 오류를 검색하십시오.  
  
 RC4 또는 RC4_128을 사용하여 대칭 키를 만들 경우 AES 알고리즘 같은 최신 암호화 기술을 선택하는 것이 좋습니다. RC4를 꼭 사용해야 할 경우에는 ALTER DATABASE SET COMPATIBILITY_LEVEL을 사용하여 데이터베이스 호환성 수준을 90 또는 100으로 설정합니다. 이 옵션은 사용하지 않는 것이 좋습니다.  
  
  
