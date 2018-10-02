---
title: SQL 메일 대신 데이터베이스 메일 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e7cde59f8406984d0e0355502df4768fe8a9af31
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815951"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>SQL 메일 대신 데이터베이스 메일 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 sys.configurations 카탈로그 뷰에서 SQL Mail XPs 서버 차원 구성 옵션이 ON으로 설정되었는지 검사합니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 SQL 메일이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 메일을 보내려면 데이터베이스 메일을 사용하십시오.  
  
 SQL 메일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대해 in-process로 실행됩니다. SQL 메일이 다운되면 서버도 다운됩니다. 데이터베이스 메일은 개별 프로세스로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부에서 실행되며, 확장 가능하고, 프로덕션 서버에 확장 MAPI 클라이언트 구성 요소를 설치할 필요가 없습니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
