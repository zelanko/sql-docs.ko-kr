---
title: MSSQLSERVER_33081 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 913be11caa9a76ee012571e5ee4b275826668330
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868587"
---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|33081|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_DLL_TRUST_VERIFICATION_FAILED|  
|메시지 텍스트|잘못된 Authenticode 서명 또는 잘못된 파일 경로로 인해 암호화 공급자 '%.*ls'을(를) 로드하지 못했습니다.  다른 오류가 있는지 이전 메시지를 확인하십시오.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 위의 오류 메시지에 나열된 암호화 공급자를 로드할 수 없습니다. 이 오류는 몇 가지 Win API 오류로 인해 발생할 수 있습니다. 링 버퍼에 오류가 발생한 API의 이름과 API에서 반환한 Windows 오류 코드가 있습니다. 자세한 내용을 보려면 다음 쿼리를 사용하여 sys.dm_os_ring_buffers 뷰를 쿼리하세요.  
  
```  
SELECT * FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
```  
  
## <a name="user-action"></a>사용자 동작  
문제를 조사하려면 MSDN(https://msdn.microsoft.com/)에서 Windows 오류 코드를 검색합니다. 오류를 해결하거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS에 문의하여 자세한 정보를 확인합니다. CSS에 문의해야 할 경우 다음 정보를 수집하여 제공하면 지원 부서 직원이 문제를 해결하는 데 도움이 됩니다.  
  
-   암호화 공급자를 로드하지 못했다는 오류가 기록된 오류 로그  
  
-   다음 문의 출력 결과  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
> 링 버퍼 정보는 다시 시작하는 동안 손실될 수 있으므로 즉시 수집하십시오.  
  
