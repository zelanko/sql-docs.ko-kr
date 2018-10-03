---
title: SQL Server 이외 구독자 추가 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4da01da52e78d1ad8923633439ebe1272a519a87
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193973"
---
# <a name="add-non-sql-server-subscriber"></a>SQL Server 이외 구독자 추가
  복제에서는 Oracle 및 IBM DB2 구독자의 스냅숏 및 트랜잭션 게시에 대한 밀어넣기 구독 생성을 지원합니다.  
  
## <a name="options"></a>변수  
 **추가할 구독자 유형**  
 Oracle 구독자 또는 IBM DB2 구독자를 선택합니다. 이러한 구독자 지원에 대한 자세한 내용은 [SQL Server 이외 구독자](non-sql/non-sql-server-subscribers.md)를 참조하세요.  
  
 **데이터 원본 이름**  
 네트워크에서 데이터베이스를 찾는 데 사용되는 이름입니다. 복제에서는 로그인, 암호 및 이 마법사의 **배포 에이전트 보안** 페이지에서 지정한 연결 옵션과 결합된 데이터 원본 이름을 사용하여 데이터베이스에 대한 연결 문자열을 생성합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 배포 에이전트가 구독을 초기화할 때까지 데이터 원본 이름과 연결 문자열의 유효성을 검사하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 이외 구독자에 대한 구독 만들기](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [게시 구독](subscribe-to-publications.md)  
  
  
