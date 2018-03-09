---
title: "정책 관리자에 정책 실패를 알리도록 경고 구성 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 235dd81e7a742635c0e289d06fa951e3965844cb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>정책 관리자에서 정책 실패를 알리도록 경고 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 정책 기반 관리 정책이 세 가지 자동 평가 모드 중 하나로 실행된 경우 정책 위반이 발생하면 이벤트 로그에 메시지가 기록됩니다. 이 메시지가 이벤트 로그에 기록되는 경우 알림을 받으려면 메시지를 검색하고 동작을 수행하도록 경고를 만듭니다. 경고는 다음 표에서와 같이 메시지를 검색해야 합니다.  
  
|실행 모드|메시지 번호|  
|--------------------|--------------------|  
|변경 시: 방지<br /><br /> (자동인 경우)|34050|  
|변경 시: 방지<br /><br /> (요청 시)|34051|  
|예약 시|34052|  
|변경 시|34053|  
  
 정책 기반 관리 오류 메시지에 응답하도록 경고를 설정하려면 다음 항목을 참조하십시오.  
  
-   [운영자 만들기](http://msdn.microsoft.com/library/1359d790-5905-4927-a208-e7155e7768a2)  
  
-   [오류 번호를 사용하여 경고 만들기](http://msdn.microsoft.com/library/03dd7fac-5073-4f86-babd-37e45a86023c)  
  
-   [운영자에게 경고 할당](http://msdn.microsoft.com/library/aa818155-6fa2-4565-a09f-5c7e31c89754)  
  
## <a name="permissions"></a>사용 권한  
 정책이 요청 시 평가되면 사용자의 보안 컨텍스트에서 실행됩니다. 오류 로그에 작성하려면 사용자가 ALTER TRACE 권한을 가지고 있거나 sysadmin 고정 서버 역할의 멤버여야 합니다. 적은 권한의 사용자가 평가하는 정책은 이벤트 로그에 작성되지 않고 경고를 발생시키지 않습니다.  
  
 자동화된 실행 모드는 sysadmin 역할의 멤버로 실행합니다. 그러면 정책에서 오류 로그 기록 및 경고 발생을 수행할 수 있습니다.  
  
## <a name="additional-considerations-about-alerts"></a>경고에 대한 추가 고려 사항  
 경고에 대한 다음 추가 고려 사항에 유의하십시오.  
  
-   경고는 설정된 정책에 대해서만 발생합니다. **요청 시** 정책을 설정할 수 없으므로 요청 시 실행되는 정책에 대해서는 경고가 발생하지 않습니다.  
  
-   전자 메일 메시지 보내기와 같은 동작을 수행하려는 경우 메일 계정을 구성해야 합니다. 데이터베이스 메일을 사용하는 것이 좋습니다. 데이터베이스 메일을 설정하는 방법에 대한 자세한 내용은 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)를 참조하세요.  
  
  
