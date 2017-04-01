---
title: "데이터베이스 무결성 검사 태스크 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.checkdatabaseintegritytask.f1"
helpviewer_keywords: 
  - "데이터 무결성 [Integration Services]"
  - "데이터베이스 무결성 검사 태스크 [Integration Services]"
  - "데이터베이스 일관성 검사"
  - "데이터베이스 일관성 검사 [Integration Services]"
  - "데이터베이스 일관성 확인"
  - "무결성 검사 [Integration Services]"
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# 데이터베이스 무결성 검사 태스크
  데이터 무결성 검사 태스크는 지정한 데이터베이스에서 모든 개체의 할당과 구조적 무결성을 검사합니다. 단일 데이터베이스나 여러 개의 데이터베이스를 검사할 수 있으며 데이터베이스 인덱스 검사 여부도 선택할 수 있습니다.  
  
 데이터베이스 무결성 검사 태스크는 DBCC CHECKDB 문을 캡슐화합니다. 자세한 내용은 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 참조하세요.  
  
## 데이터베이스 무결성 검사 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [데이터베이스 무결성 검사 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  