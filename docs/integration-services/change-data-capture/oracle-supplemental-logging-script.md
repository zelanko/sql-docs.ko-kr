---
title: "Oracle 보완 로깅 스크립트 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e6ee618-b89b-46c7-92ad-4fc5ef7b777a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4f97617decf23356dc663805494d5a2d9e2d72c
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="oracle-supplemental-logging-script"></a>Oracle 보완 로깅 스크립트
  이 대화 상자에는 Oracle 보완 로깅 스크립트가 표시됩니다.  
  
 사용할 CDC 인스턴스를 준비할 때 CDC Designer는 캡처할 테이블에 대한 보완 로깅을 설정하는 Oracle SQL 스크립트를 만듭니다. 보완 로깅 스크립트는 특정 테이블이 업데이트될 경우 트랜잭션 로그에 기록되는 변경 레코드에 변경된 열뿐만 아니라 관련 열의 데이터도 모두 포함되도록 Oracle에 지시합니다.  
  
 조직의 Oracle DBA 정책에 따라 보완 로깅 스크립트를 실행하려면 Oracle DBA의 검토와 승인이 필요할 수 있습니다.  
  
## <a name="options"></a>변수  
 다음은 스크립트를 실행하는 방법을 지정하는 데 사용할 수 있는 옵션입니다.  
  
 **스크립트 실행**  
 CDC 인스턴스에 대해 정의된 테이블에서 보완 로깅 스크립트를 실행합니다. 이 스크립트를 실행하려면 캡처할 모든 테이블에 대한 ALTER TABLE 권한과 DBA_LOG_GROUPS 뷰에 대한 SELECT 권한이 Oracle 사용자에게 있어야 합니다. 또한 Oracle 사용자에게 필요한 사용 권한과 함께 Oracle 데이터베이스 사용을 위한 자격 증명이 있어야 합니다. 프로그램에서 Oracle 자격 증명을 묻는 메시지를 표시한 다음 스크립트를 실행하도록 할 수 있습니다.  
  
 **다른 이름으로 저장**  
 스크립트를 텍스트 파일에 저장합니다. Oracle 데이터베이스 관리자(DBA)가 보완 로깅 스크립트를 검사하고 실행해야 하는 경우에 사용되며, 스크립트를 텍스트 파일로 저장하여 나중에 전자 메일 또는 다른 방법으로 Oracle DBA에게 보낸 다음 Oracle 데이터베이스에서 스크립트를 실행하는 데 사용되는 SQL*Plus Oracle 유틸리티 또는 기타 도구를 사용하여 스크립트를 실행할 수 있습니다.  
  
 **복사**  
 스크립트를 클립보드에 복사합니다. Oracle 데이터베이스 관리자가 보완 로깅 스크립트를 검사하고 실행해야 하는 경우에 필요한 위치에 스크립트를 붙여 넣을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC 인스턴스 관리 방법](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [CDC 인스턴스 관리](../../integration-services/change-data-capture/manage-a-cdc-instance.md)  
  
  
