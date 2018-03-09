---
title: "데이터베이스 속성(트랜잭션 로그 전달 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1016bfa1e560c6ec9b4db1db393e4c44366cae16
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-transaction-log-shipping-page"></a>데이터베이스 속성(트랜잭션 로그 전달 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 페이지를 사용하여 데이터베이스의 로그 전달 속성을 구성하고 수정할 수 있습니다.  
  
 로그 전달 개념에 대한 설명은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **이 데이터베이스를 로그 전달 구성의 주 데이터베이스로 사용**  
 이 데이터베이스를 로그 전달 주 데이터베이스로 사용합니다. 이 옵션을 선택한 다음 페이지의 나머지 옵션을 구성합니다. 이 확인란의 선택을 취소하면 이 데이터베이스의 로그 전달 구성이 삭제됩니다.  
  
 **백업 설정**  
 백업 일정, 위치, 경고 및 보관 매개 변수를 구성하려면 **백업 설정** 을 클릭합니다.  
  
 **백업 일정**  
 주 데이터베이스에 대해 현재 선택한 백업 일정을 보여 줍니다. 이러한 설정을 수정하려면 **백업 설정** 을 클릭합니다.  
  
 **마지막으로 백업을 만든 날짜**  
 주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업의 시간과 날짜를 나타냅니다.  
  
 **보조 서버 인스턴스 및 데이터베이스**  
 이 주 데이터베이스에 대해 현재 구성된 보조 서버와 데이터베이스를 나열합니다. 해당 보조 데이터베이스와 연결된 매개 변수를 수정하려면 데이터베이스를 강조 표시한 다음 **...** 을 클릭합니다.  
  
 **추가**  
 이 주 데이터베이스의 로그 전달 구성에 보조 데이터베이스를 추가하려면 **추가** 를 클릭합니다.  
  
 **제거**  
 이 로그 전달 구성에서 선택한 데이터베이스를 제거합니다. 먼저 데이터베이스를 선택한 다음 **제거**를 클릭합니다.  
  
 **모니터 서버 인스턴스 사용**  
 이 로그 전달 구성에 대한 모니터 서버 인스턴스를 설정합니다. 모니터 서버 인스턴스를 지정하려면 **모니터 서버 인스턴스 사용** 확인란을 선택한 다음 **설정** 을 클릭합니다.  
  
 **모니터 서버 인스턴스**  
 이 로그 전달 구성에 대해 현재 구성된 모니터 서버 인스턴스를 나타냅니다.  
  
 **설정**  
 로그 전달 구성에 대한 모니터 서버 인스턴스를 구성합니다. 이 모니터 서버 인스턴스를 구성하려면 **설정** 을 클릭합니다.  
  
 **구성 스크립팅**  
 선택한 매개 변수로 로그 전달을 구성하기 위한 스크립트를 생성합니다. **구성 스크립팅**을 클릭한 다음 스크립트의 출력 대상을 선택합니다.  
  
> [!IMPORTANT]  
>  보조 데이터베이스에 대한 설정을 스크립팅하기 전에 **보조 데이터베이스 설정** 대화 상자를 호출해야 합니다. 이 대화 상자를 호출하면 보조 서버에 연결되며 스크립트 생성에 필요한 보조 데이터베이스의 현재 설정이 검색됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)   
 [로그 전달 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
