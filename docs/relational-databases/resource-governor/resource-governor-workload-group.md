---
title: "리소스 관리자 작업 그룹 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "리소스 관리자, 작업 그룹"
  - "작업 그룹 [SQL Server]"
  - "작업 그룹 [SQL Server], 개요"
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 리소스 관리자 작업 그룹
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 관리자에서 작업 그룹은 분류 기준이 유사한 세션 요청에 대한 컨테이너의 역할을 합니다. 작업 그룹을 사용하면 세션의 집계 모니터링이 가능하며 작업 그룹으로 세션의 정책을 정의할 수 있습니다. 각 작업 그룹은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 물리적 리소스의 하위 집합을 나타내는 리소스 풀에 있습니다. 세션이 시작되면 리소스 관리자 분류자가 세션을 특정 작업 그룹에 할당하고, 세션은 작업 그룹에 할당된 정책 및 리소스 풀에 정의된 리소스를 사용하여 실행해야 합니다.  
  
## 작업 그룹 개념  
 작업 그룹은 각 요청에 적용되는 분류 조건에 따라 유사한 세션 요청의 컨테이너 역할을 수행합니다. 작업 그룹을 사용하면 리소스 소비에 대해 집계 모니터링을 수행하고 그룹에 있는 모든 요청에 단일 정책을 적용할 수 있습니다. 그룹은 해당 멤버에 대한 정책을 정의합니다.  
  
> [!NOTE]  
>  사용자 정의 작업 그룹은 한 리소스 풀에서 다른 리소스 풀로 이동할 수 있습니다.  
  
 리소스 관리자는 내부 그룹과 기본 그룹이라는 두 개의 작업 그룹을 미리 정의합니다. 사용자는 내부 그룹으로 분류된 그룹을 변경할 수 없지만 모니터링은 할 수 있습니다. 다음 조건에 해당하는 경우 요청은 기본 그룹으로 분류됩니다.  
  
-   요청을 분류할 조건이 없습니다.  
  
-   존재하지 않는 그룹으로 요청을 분류하려는 시도가 있습니다.  
  
-   일반 분류 실패가 있습니다.  
  
 리소스 관리자는 작업 그룹을 생성, 변경 및 삭제하는 DDL 문도 제공합니다.  
  
## 작업 그룹 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|작업 그룹을 만드는 방법에 대해 설명합니다.|[작업 그룹 만들기](../../relational-databases/resource-governor/create-a-workload-group.md)|  
|작업 그룹을 설정을 변경하는 방법에 대해 설명합니다.|[작업 그룹 설정 변경](../../relational-databases/resource-governor/change-workload-group-settings.md)|  
|작업 그룹을 삭제하는 방법에 대해 설명합니다.|[작업 그룹 삭제](../../relational-databases/resource-governor/delete-a-workload-group.md)|  
  
## 참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [템플릿을 사용하여 리소스 관리자 구성](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [리소스 관리자 속성 보기](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  