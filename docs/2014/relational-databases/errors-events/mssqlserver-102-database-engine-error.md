---
title: MSSQLSERVER_102 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac4f4d6c19eb58e9e1eb9b2eb71312f001aa5f6b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969863"
---
# <a name="mssqlserver_102"></a>MSSQLSERVER_102
    
## <a name="details"></a>세부 정보  
  
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
  
  
