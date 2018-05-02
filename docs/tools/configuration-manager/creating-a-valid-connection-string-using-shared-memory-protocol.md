---
title: 공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fd43bed97059b2b2e6dcff4b921b31f30f07f18
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  클라이언트가 클라이언트와 동일한 컴퓨터에서 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 때는 공유 메모리 프로토콜을 사용합니다. 공유 메모리의 속성은 구성할 수 없습니다. 공유 메모리는 항상 가장 먼저 사용하려고 시도하며 **클라이언트 프로토콜 속성** 목록의 **사용할 수 있는 프로토콜** 목록 맨 위에서 다른 위치로 이동할 수 없습니다. 공유 메모리 프로토콜을 사용하지 않으면 다른 프로토콜의 문제를 해결할 때 편리합니다.  
  
 공유 메모리 프로토콜을 사용하여 별칭을 만들 수는 없지만 공유 메모리를 사용하는 경우 이름으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결하면 공유 메모리 연결이 생성됩니다. 공유 메모리 연결 문자열은 `lpc:<servername>[\instancename]`형식을 사용합니다.  
  
## <a name="connecting-to-the-local-server"></a>로컬 서버에 연결  
 클라이언트와 동일한 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 때는 서버 이름으로 **(local)** 을 사용할 수 있습니다. 이 방법은 모호성을 유발하므로 권장되지 않지만 클라이언트가 어떤 컴퓨터에서 실행될지 알고 있는 경우에는 유용할 수 있습니다. 예를 들어 영업 사원과 같이 네트워크에 연결되지 않은 모바일 사용자를 위해 응용 프로그램을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 랩톱 컴퓨터에서 실행되고 프로젝트 데이터를 저장하는 경우 **(local)** 에 연결하는 클라이언트는 항상 랩톱에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결됩니다. 단어 **localhost** 또는 마침표(**.**)를 **(local)** 대신 사용할 수 있습니다.  
  
## <a name="verifying-your-connection-protocol"></a>연결 프로토콜 확인  
 다음 쿼리는 현재 연결에 사용된 프로토콜을 반환합니다.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>예:  
 다음 이름은 로컬 컴퓨터에 연결할 때 공유 메모리 프로토콜을 사용합니다(사용하는 경우).  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 공유 메모리 연결에 대해서는 별칭을 만들 수 없습니다.  
  
> [!NOTE]  
>  **서버** 상자에 IP 주소를 지정하면 TCP/IP 연결이 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)   
 [네트워크 프로토콜 선택](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
