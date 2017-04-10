---
title: "패키지 역할 대화 상자 UI 참조 | Microsoft Docs"
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
  - "sql13.dts.dtsserver.packageroles.f1"
helpviewer_keywords: 
  - "패키지 역할 대화 상자"
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# 패키지 역할 대화 상자 UI 참조
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있는 **패키지 역할** 대화 상자를 통해 패키지에 대한 읽기 권한이 있는 데이터베이스 수준 역할 및 패키지에 대한 쓰기 권한이 있는 데이터베이스 수준 역할을 지정할 수 있습니다. 데이터베이스 수준 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스에 저장된 패키지에만 적용됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 수준 역할과 해당 사용 권한에 대한 자세한 내용은 [Integration Services 역할&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-roles-ssis-service.md)을 참조하세요.  
  
 대화 상자에 나열된 역할은 **msdb** 시스템 데이터베이스의 현재 데이터베이스 역할입니다. 역할을 선택하지 않으면 기본 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 역할이 적용됩니다. 기본적으로 읽기 역할에는 **db_ssisadmin**, **db_ssisoperator** 및 패키지를 만든 사용자가 포함됩니다. 이러한 역할 중 하나의 멤버이거나 패키지를 만든 사용자는 패키지를 열거, 확인, 내보내기 및 실행할 수 있습니다. 기본적으로 쓰기 역할에는 **db_ssisadmin**과 패키지를 만든 사용자가 포함됩니다. 이 역할의 멤버인 사용자와 패키지를 만든 사용자는 패키지를 가져오거나 삭제 및 변경할 수 있습니다.  
  
 **sysssispackages** 테이블의 **ownersid** 열은 패키지를 만든 사용자의 고유 보안 식별자를 표시합니다.  
  
## 옵션  
 **패키지 이름**  
 패키지의 이름을 지정합니다.  
  
 **읽기 역할**  
 목록에서 역할을 선택합니다.  
  
 **쓰기 역할**  
 목록에서 역할을 선택합니다.  
  
## 관련 항목:  
 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [보안 개요&#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  