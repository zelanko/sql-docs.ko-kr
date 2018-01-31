---
title: "T-SQL 문 실행 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec1d7b5264d880b3cec0ec8b6348441e89147d6c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="execute-t-sql-statement-task"></a>T-SQL 문 실행 태스크
  T-SQL 문 실행 태스크는 Transact-SQL 문을 실행합니다. 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](../../t-sql/transact-sql-reference-database-engine.md) 및 [Integration Services&#40;SSIS&#41; 쿼리](../../integration-services/integration-services-ssis-queries.md)를 참조하세요.  
  
 이 태스크는 SQL 실행 태스크와 유사합니다. 그러나 T-SQL 문 실행 태스크는 SQL 언어의 Transact-SQL 버전만 지원하며 이 태스크를 사용하여 SQL 언어의 다른 언어를 사용하는 문을 서버에서 실행할 수 없습니다. 매개 변수가 있는 쿼리를 실행하거나 쿼리 결과를 변수에 저장하거나 속성 식을 사용해야 하는 경우 T-SQL 문 실행 태스크 대신 SQL 실행 태스크를 사용해야 합니다. 자세한 내용은 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)을 참조하세요.  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>T-SQL 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [T-SQL 문 실행 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)   
 [Integration Services 패키지의 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
  
