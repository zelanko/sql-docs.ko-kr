---
title: "유지 관리 계획(보고 및 로깅 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.maint.reportinglogging.f1"
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# 유지 관리 계획(보고 및 로깅 페이지)
  **보고 및 로깅** 대화 상자를 사용하여 유지 관리 계획이 실행될 때 생성되는 보고서와 로그를 구성할 수 있습니다.  
  
## 옵션  
 **텍스트 파일 보고서 생성**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 텍스트 파일 보고서를 기록하도록 할지 여부를 지정합니다.  
  
 **새 파일 만들기**  
 유지 관리 계획이 실행될 때마다 새 보고서 파일을 만듭니다. 기본적으로 보고서 파일은 해당 유지 관리 계획이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터의 기본 로그 폴더에 기록됩니다. 기본 로그 폴더는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중 설정합니다. 다른 폴더를 지정하려면 **폴더** 입력란에 전체 폴더 경로를 입력하거나 찾아보기 단추(**...**)를 클릭하고 원하는 폴더를 탐색합니다.  
  
 **파일에 추가**  
 각각의 계획을 실행하여 생성된 보고서를 **파일 이름** 입력란에 지정된 파일에 추가합니다. 찾아보기 단추를 클릭하고 대화 상자에서 파일을 선택하여 파일을 지정할 수도 있습니다.  
  
 **전자 메일 받는 사람에게 보고서 보내기**  
 유지 관리 계획의 실행 결과를 전자 메일로 보냅니다. 이 옵션은 데이터베이스 메일을 활성화하고 적절히 구성한 경우에만 사용할 수 있습니다.  
  
 **에이전트 운영자**  
 전자 메일을 받는 에이전트 운영자를 목록에서 선택합니다. 이 옵션은 메일을 활성화하고 적절히 구성한 경우에만 사용할 수 있습니다.  
  
 **확장 정보 기록**  
 로그에 추가 정보를 포함합니다. 이 옵션을 선택하면 저장되는 유지 관리 계획 기록의 크기가 커집니다.  
  
 **원격 서버에 기록**  
 원격 서버에 유지 관리 계획 기록을 작성합니다.  
  
 **연결**  
 원격 서버에 기록할 때 사용할 연결 정보를 지정합니다.  
  
 **새로 만들기**  
 **연결 속성** 대화 상자를 표시합니다. 원격 서버에 기록할 때 사용할 새 연결 정보를 구성하는 데 사용됩니다.  
  
## 참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
  