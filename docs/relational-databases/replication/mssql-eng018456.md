---
title: "MSSQL_ENG018456 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 03184d93644598527b76f054051c66f92ecc6d3e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18456|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|사용자 '%.*ls'이(가) 로그인하지 못했습니다.%.\*ls|  
  
## <a name="explanation"></a>설명  
 로그인 시도가 실패할 때마다 MSSQL_ENG018456 오류가 발생합니다. 오류 메시지에 **distributor_admin** 계정이 포함된 경우(사용자 'distributor_admin'이 로그인하지 못했습니다 등) 복제에 사용된 계정에 문제가 있는 것입니다. 복제는 원격 서버 **repl_distributor**를 만들어 배포자와 게시자 간 통신을 허용합니다. 로그인 **distributor_admin** 은 이 원격 서버와 연결되며 유효한 암호가 지정되어야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 계정의 암호를 지정했는지 확인하십시오. 자세한 내용은 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

