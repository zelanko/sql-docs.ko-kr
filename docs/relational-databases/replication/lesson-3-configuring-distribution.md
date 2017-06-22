---
title: "3단원: 배포 구성 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e582c5fb7853c69a083755a944bd3922d0d4c5af
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-configuring-distribution"></a>3단원: 배포 구성
이 단원에서는 게시자에서 배포를 구성하고 게시 및 배포 데이터베이스에서 필수 사용 권한을 설정합니다. 배포자를 이미 구성한 경우 이 단원을 시작하기 전에 우선 게시와 배포를 해제해야 합니다. 기존 복제 토폴로지를 유지해야 하는 경우에는 이 작업을 수행하지 마십시오.  
  
원격 배포자를 사용한 게시자 구성은 이 자습서의 범위를 벗어납니다.  
  
### <a name="configuring-distribution-at-the-publisher"></a>게시자에서 배포 구성  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **배포 구성**을 클릭합니다.  
  
    > [!NOTE]  
    > 실제 서버 이름이 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localhost **를 사용하여** 에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 **'localhost'**서버에 연결할 수 없다는 경고가 표시됩니다. 경고 대화 상자에서 **확인** 을 클릭합니다. **서버에 연결** 대화 상자에서 **서버 이름** 을 **localhost** 에서 실제 서버 이름으로 변경합니다. **연결**을 클릭합니다.  
  
    배포 구성 마법사가 시작됩니다.  
  
3.  **배포자** 페이지에서 ['ServerName'을(를) 자체 배포자로 사용합니다. SQL Server에서 배포 데이터베이스와 로그를 만듭니다.**]를 선택하고 **다음**을 클릭합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행되고 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**에이전트 시작** 페이지에서 **예**를 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작되도록 구성합니다. **다음**을 클릭합니다.  
  
5.  **스냅숏 폴더** 입력란에 **\\\\**\<*Machine_Name>***\repldata**를 입력하고 **다음**을 클릭합니다. 여기서 \<*Machine_Name>*은 게시자의 이름입니다.  
  
6.  마법사의 나머지 페이지에 기본값을 적용합니다.  
  
7.  **마침** 을 클릭하여 배포를 사용하도록 설정합니다.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>게시자에서 데이터베이스 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.  
  
2.  **일반** 페이지에서 **검색**을 클릭하고 **선택할 개체 이름 입력** 상자에 \<*Machine_Name>***\repl_snapshot**을 입력한 다음 **이름 확인**, **확인**을 차례로 클릭합니다. 여기서 \<*Machine_Name>*은 로컬 게시자 서버의 이름입니다.  
  
3.  **사용자 매핑** 페이지의 **이 로그인으로 매핑된 사용자** 목록에서 **배포** 및 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 둘 다 선택합니다.  
  
    **데이터베이스 역할 멤버 자격** 목록에서 두 데이터베이스의 로그인에 대해 **db_owner** 역할을 선택합니다.  
  
4.  **확인** 을 클릭하여 로그인을 만듭니다.  
  
5.  1-4단계를 반복하여 로컬 repl_logreader 계정에 대한 로그인을 만듭니다. 이 로그인은 **배포** 와 **AdventureWorks** 데이터베이스에서 **db_owner** 고정 데이터베이스 역할의 멤버인 사용자에게도 매핑되어야 합니다.  
  
6.  1-4단계를 반복하여 로컬 repl_distribution 계정에 대한 로그인을 만듭니다. 이 로그인은 **배포** 데이터베이스에서 **db_owner** 고정 데이터베이스 역할의 멤버인 사용자에게 매핑되어야 합니다.  
  
7.  1-4단계를 반복하여 로컬 repl_merge 계정에 대한 로그인을 만듭니다. 이 로그인에는 **배포** 와 **AdventureWorks** 데이터베이스의 사용자 매핑이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[배포 구성](../../relational-databases/replication/configure-distribution.md)  
[복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)  
  
  
  

