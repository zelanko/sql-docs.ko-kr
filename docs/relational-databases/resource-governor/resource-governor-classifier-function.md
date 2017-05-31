---
title: "리소스 관리자 분류자 함수 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 284ee7a05af7ab73e78dd827269db49c7d3f1e00
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="resource-governor-classifier-function"></a>리소스 관리자 분류자 함수
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 관리자 분류 프로세스는 세션 특징에 기초하여 들어오는 세션을 작업 그룹에 할당합니다. 분류자 함수라고 하는 사용자 정의 함수를 작성하여 원하는 분류 논리를 지정할 수 있습니다.  
  
## <a name="classification"></a>분류  
 리소스 관리자는 들어오는 세션의 분류를 지원합니다. 분류는 함수에 포함된 사용자 작성 조건 집합을 기준으로 합니다. 함수 논리의 결과는 리소스 관리자가 세션을 기존 작업 그룹으로 분류할 수 있도록 합니다.  
  
> [!NOTE]  
>  내부 작업 그룹은 내부 전용 요청으로 채워집니다. 이러한 요청을 라우팅하는 데 사용되는 조건은 변경할 수 없으며, 요청을 내부 작업 그룹으로 분류할 수 없습니다.  
  
 들어오는 세션을 작업 그룹에 할당하는 데 사용되는 논리가 포함된 스칼라 함수를 작성할 수 있습니다. 이 함수를 사용하려면 우선 다음 동작을 완료해야 합니다.  
  
-   ALTER RESOURCE GOVERNOR 문을 사용하여 함수를 만들고 등록합니다. 자세한 내용은 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)를 참조하세요.  
  
-   ALTER RESOURCE GOVERNOR 문을 RECONFIGURE 매개 변수와 함께 사용하여 리소스 관리자 구성을 업데이트합니다.  
  
 함수를 만들고 구성 변경 내용을 적용하면 리소스 관리자 분류자는 함수에서 반환한 작업 그룹 이름을 사용하여 적절한 작업 그룹으로 새 요청을 보냅니다.  
  
> [!IMPORTANT]  
>  지정된 로그인 제한 시간 내에 분류 함수가 완료되지 않으면 클라이언트 세션이 시간 초과될 수 있습니다. 로그인 시간 제한은 클라이언트 속성이기 때문에 서버에서는 시간 제한을 인식하지 못합니다. 장기 실행 분류자 함수는 서버를 오랫동안 연결되지 않은 상태로 둘 수 있습니다. 따라서 연결 시간 제한 전에 실행을 종료하는 분류자 함수를 만들어야 합니다.  
  
 사용자 정의 함수에는 다음과 같은 특징과 동작이 있습니다.  
  
-   사용자 정의 함수는 모든 새 세션에 대해 평가됩니다. 연결 풀링이 사용되는 경우에도 마찬가지입니다.  
  
-   사용자 정의 함수는 세션에 작업 그룹 컨텍스트를 제공합니다. 그룹 멤버가 확인되면 세션은 세션이 사용되는 기간 동안 작업 그룹에 바인딩됩니다.  
  
-   사용자 정의 함수가 NULL, 기본값 또는 존재하지 않는 그룹의 이름을 반환하면 기본 작업 그룹 컨텍스트가 세션에 제공됩니다. 또한 어떤 이유로든 함수가 실패하는 경우에도 세션에 기본 컨텍스트가 제공됩니다.  
  
-   함수는 서버 범위(master 데이터베이스)로 정의되어야 합니다.  
  
-   분류자 사용자 정의 함수 지정은 ALTER RESOURCE GOVERNOR RECONFIGURE가 실행된 후에만 적용됩니다.  
  
-   한 번에 하나의 사용자 정의 함수만 분류자로 지정될 수 있습니다.  
  
-   해당 분류자 상태가 제거되지 않는 한 분류자 사용자 정의 함수는 삭제하거나 변경할 수 없습니다.  
  
-   분류자 사용자 정의 함수가 없으면 모든 세션이 기본 그룹으로 분류됩니다.  
  
-   분류자 함수에서 반환한 작업 그룹은 스키마 바인딩 제한의 범위를 벗어납니다. 예를 들어 테이블은 삭제할 수 없지만 작업 그룹은 삭제할 수 있습니다.  
  
> [!IMPORTANT]  
>  서버에서 DAC(관리자 전용 연결)를 사용하는 것이 좋습니다. DAC는 리소스 관리자 분류의 영향을 받지 않으며 분류자 함수의 모니터링 및 문제 해결에 사용할 수 있습니다. 자세한 내용은 [데이터베이스 관리자를 위한 진단 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하세요. 문제 해결에 DAC를 사용할 수 없는 경우 사용 가능한 다른 방법은 단일 사용자 모드로 시스템을 다시 시작하는 것입니다. 단일 사용자 모드는 분류의 영향을 받지 않지만 이렇게 해도 리소스 관리자 분류가 실행 중일 때 이를 진단하는 기능은 제공되지 않습니다.  
  
### <a name="classification-process"></a>분류 프로세스  
 리소스 관리자 컨텍스트에서 세션에 대한 로그인 프로세스는 다음 단계로 구성됩니다.  
  
1.  로그인 인증  
  
2.  LOGON 트리거 실행  
  
3.  분류  
  
 분류가 시작되면 리소스 관리자는 분류자 함수를 실행하고 이 함수에서 반환된 값을 사용하여 적절한 작업 그룹으로 요청을 보냅니다.  
  
> [!NOTE]  
>  분류자 함수 및 LOGON 트리거 실행에 대한 자세한 내용은 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 및 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조하세요.  
  
## <a name="classification-function-tasks"></a>분류 함수 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|분류자 사용자 정의 함수를 만들고 테스트하는 방법에 대해 설명합니다.|[분류자 사용자 정의 함수 만들기 및 테스트](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [템플릿을 사용하여 리소스 관리자 구성](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [리소스 관리자 속성 보기](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
