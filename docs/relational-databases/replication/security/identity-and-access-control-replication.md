---
title: "ID 및 액세스 제어(복제) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "액세스 제어 [SQL Server 복제]"
  - "보안 [SQL Server 복제], ID 및 액세스 제어"
  - "인증 [SQL Server 복제]"
  - "ID [복제]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# ID 및 액세스 제어(복제)
  인증은 기준이 엔터티 (일반적으로이 컨텍스트에서 컴퓨터) 라고도 하는 다른 엔터티를 확인 하는 프로세스는 *주*, 되도록 맞는지 (일반적으로 다른 컴퓨터 또는 사용자)가 있습니다. 권한 부여는 파일 시스템의 파일이나 데이터베이스의 테이블과 같은 리소스에 대한 액세스 권한을 인증된 보안 주체에게 부여하는 프로세스입니다.  
  
 복제 보안은 인증 및 권한 부여를 사용하여 복제된 데이터베이스 개체 및 복제 처리와 관련된 컴퓨터와 에이전트에 대한 액세스를 제어합니다. 이 작업은 다음과 같은 3가지 메커니즘을 통해 수행됩니다.  
  
-   에이전트 보안  
  
     복제 에이전트 보안 모델을 사용하여 복제 에이전트를 실행 및 연결하는 계정을 더욱 세밀하게 제어할 수 있습니다. 에이전트 보안 모델에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오. 에이전트에 대 한 로그인 및 암호 설정 하는 방법에 대 한 정보를 참조 하십시오. [복제의 관리 로그인 및 암호](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)합니다.  
  
-   관리 역할  
  
     복제 설정, 유지 관리 및 처리에 올바른 서버 및 데이터베이스 역할이 사용되도록 합니다. 자세한 내용은 [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md)을(를) 참조하세요.  
  
-   PAL(게시 액세스 목록)  
  
     PAL을 통해 게시에 대한 액세스 권한을 부여합니다. PAL 기능은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 액세스 제어 목록과 유사하게 작동합니다. 구독자가 게시자 또는 배포자에 연결하여 게시에 대한 액세스를 요청하면 에이전트가 전달한 인증 정보가 PAL과 비교됩니다. 자세한 내용 및 PAL에 대 한 모범 사례에 대 한 참조 [게시자 보안 설정](../../../relational-databases/replication/security/secure-the-publisher.md)합니다.  
  
## 게시된 데이터 필터링  
 인증 및 권한 부여를 통해 복제된 데이터 및 개체에 대한 액세스를 제어하는 옵션 외에도 복제에는 구독자에서 사용 가능한 데이터를 제어하는 두 가지 옵션, 즉 열 필터링과 행 필터링이 있습니다. 필터링에 대 한 자세한 내용은 참조 [데이터를 게시 하는 필터](../../../relational-databases/replication/publish/filter-published-data.md)합니다.  
  
 아티클을 정의할 때는 게시에 필요한 열만 게시하고 불필요하거나 중요한 데이터를 포함하는 열은 생략할 수 있습니다. 예를 들어 Adventure Works 데이터베이스의 **Customer** 테이블을 현장에 있는 영업 담당자에게 게시하는 경우 회사 중역에게만 필요한 **AnnualSales** 열은 생략할 수 있습니다.  
  
 게시된 데이터를 필터링하여 데이터에 대한 액세스를 제한할 수 있고 구독자에서 사용 가능한 데이터를 지정할 수 있습니다. 예를 들어 **Customer** 테이블을 필터링하여 협력사에서는 **ShareInfo** 열의 값이 "예"인 고객에 대한 정보만 받도록 할 수 있습니다. 병합 복제에서 HOST_NAME()을 포함하는 매개 변수가 있는 필터를 사용할 경우 보안 고려 사항이 있습니다. 자세한 내용을 보려면의 "필터링으로 host_name ()" 섹션을 참조 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)합니다.  
  
## 참고 항목  
 [보안 및 보호 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [보안 개요 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [위협 및 취약성 완화 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  