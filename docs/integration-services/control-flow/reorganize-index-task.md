---
title: "인덱스 다시 구성 태스크 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.reorganizeindextask.f1"
helpviewer_keywords: 
  - "인덱스 다시 구성"
  - "인덱스 다시 구성 태스크 [Integration Services]"
  - "인덱스 [Integration Services]"
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# 인덱스 다시 구성 태스크
  인덱스 다시 구성 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 테이블과 뷰의 인덱스를 다시 구성합니다. 인덱스 관리에 대한 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
 인덱스 다시 구성 태스크를 사용하면 패키지가 단일 데이터베이스나 여러 데이터베이스의 인덱스를 다시 구성할 수 있습니다. 태스크가 단일 데이터베이스의 인덱스만 다시 구성하는 경우 인덱스를 다시 구성할 뷰와 테이블을 선택할 수 있습니다. 인덱스 다시 구성 태스크에는 큰 개체 데이터를 압축하는 옵션도 포함되어 있습니다. 큰 개체 데이터는 **image**, **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** 또는 **xml** 데이터 형식의 데이터입니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
 인덱스 다시 구성 태스크는 Transact-SQL ALTER INDEX 문을 캡슐화합니다. 큰 개체 데이터를 압축하도록 선택하면 이 문은 REORGANIZE WITH (LOB_COMPACTION = ON) 절을 사용하고 그렇지 않으면 LOB_COMPACTION이 OFF로 설정됩니다. 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  태스크에서 실행할 Transact-SQL 문을 만드는 데 걸리는 시간은 태스크에서 다시 구성하는 인덱스 수에 비례합니다. 많은 수의 인덱스가 있는 데이터베이스의 모든 테이블과 뷰의 인덱스를 다시 구성하거나 여러 데이터베이스의 인덱스를 다시 구성하도록 태스크를 구성하면 Transact-SQL 문을 생성하는 데 시간이 오래 걸릴 수 있습니다.  
  
## 인덱스 다시 구성 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [인덱스 다시 구성 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## 관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)을 참조하세요.  
  
## 관련 항목:  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  