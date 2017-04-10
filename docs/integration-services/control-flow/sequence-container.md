---
title: "시퀀스 컨테이너 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sequencecontainer.f1"
helpviewer_keywords: 
  - "시퀀스 컨테이너"
  - "제어 흐름 그룹화"
  - "컨테이너 [Integration Services], 시퀀스"
  - "제어 흐름의 하위 집합 [Integration Services]"
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 48
---
# 시퀀스 컨테이너
  시퀀스 컨테이너는 패키지 제어 흐름의 하위 집합인 제어 흐름을 정의합니다. 시퀀스 컨테이너는 패키지를 여러 개의 별도 제어 흐름으로 그룹화하며, 각 제어 흐름에는 전체 패키지 제어 흐름 내에서 실행되는 하나 이상의 태스크 및 컨테이너가 포함됩니다.  
  
 시퀀스 컨테이너에는 여러 태스크 외에도 다른 컨테이너를 포함시킬 수 있습니다. 시퀀스 컨테이너에 태스크 및 컨테이너를 추가하는 방법은 패키지에 추가하는 방법과 비슷하며, 태스크 및 컨테이너를 패키지 컨테이너가 아닌 시퀀스 컨테이너로 끌어 온다는 점만 다릅니다. 시퀀스 컨테이너에 두 개 이상의 태스크 또는 컨테이너가 포함된 경우 패키지에서와 같은 방식으로 선행 제약 조건을 사용하여 이를 연결할 수 있습니다. 자세한 내용은 [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md)을 참조하세요.  
  
 시퀀스 컨테이너를 사용할 경우 다음과 같은 많은 이점이 있습니다.  
  
-   패키지 제어 흐름의 특정 하위 집합에서 패키지 디버깅을 중점적으로 처리하기 위해 태스크 그룹 사용 안 함  
  
-   개별 태스크가 아닌 시퀀스 컨테이너의 속성을 설정하여 한 위치에서 여러 태스크의 속성 관리  
  
     예를 들어 시퀀스 컨테이너의 **Disable** 속성을 **True** 로 설정하여 시퀀스 컨테이너의 모든 태스크와 컨테이너를 해제할 수 있습니다.  
  
-   관련 태스크 및 컨테이너 그룹에서 사용하는 변수의 범위 제공  
  
-   시퀀스 컨테이너를 확장하거나 축소하여 보다 쉽게 관리할 수 있도록 많은 태스크 그룹화  
  
     또한 **그룹** 상자를 사용하여 확장 및 축소되는 태스크 그룹을 만들 수 있습니다. 하지만 **그룹** 상자는 디자인 타임 기능이기 때문에 속성이나 런타임 동작이 없습니다. 자세한 내용은 [구성 요소 그룹화 또는 그룹 해제](../../integration-services/group-or-ungroup-components.md)를 참조하세요.  
  
-   시퀀스 컨테이너에 트랜잭션 특성을 설정하여 패키지 제어 흐름의 하위 집합에 대한 트랜잭션을 정의할 수 있습니다. 이러한 방식으로 보다 세부적으로 트랜잭션을 관리할 수 있습니다.  
  
     예를 들어 시퀀스 컨테이너에 두 개의 관련 태스크가 포함되어 있으며 두 태스크 중 하나는 테이블의 데이터를 삭제하고 다른 태스크는 테이블에 데이터를 삽입하는 경우 삽입 동작 실패 시 삭제 동작이 롤백되도록 트랜잭션을 구성할 수 있습니다. 자세한 내용은 [Integration Services 트랜잭션](../../integration-services/integration-services-transactions.md)을 참조하세요.  
  
## 시퀀스 컨테이너 구성  
 시퀀스 컨테이너에는 사용자 지정 사용자 인터페이스가 없으며 **의** 속성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 창에서나 프로그래밍 방식으로만 구성할 수 있습니다.  
  
 프로그래밍 방식으로 이러한 속성을 설정하는 방법은 개발자 가이드에서 **T:Microsoft.SqlServer.Dts.Runtime.Sequence** 클래스에 대한 설명서를 참조하십시오.  
  
## 관련 작업  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)을 참조하세요.  
  
## 관련 항목:  
 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../Topic/Connect%20Tasks%20and%20Containers%20by%20Using%20a%20Default%20Precedence%20Constraint.md)   
 [Integration Services 컨테이너](../../integration-services/control-flow/integration-services-containers.md)  
  
  