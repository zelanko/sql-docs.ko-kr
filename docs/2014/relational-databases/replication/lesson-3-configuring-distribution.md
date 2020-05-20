---
title: '3단원: 배포 구성 | Microsoft 문서'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0a648902b97a8224b9032c24ee8c7715a4030777
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000432"
---
# <a name="lesson-3-configuring-distribution"></a>3단원: 배포 구성
  이 단원에서는 게시자에서 배포를 구성하고 게시 및 배포 데이터베이스에서 필수 사용 권한을 설정합니다. 배포자를 이미 구성한 경우 이 단원을 시작하기 전에 우선 게시와 배포를 해제해야 합니다. 기존 복제 토폴로지를 유지해야 하는 경우에는 이 작업을 수행하지 마십시오.  
  
 원격 배포자를 사용한 게시자 구성은 이 자습서의 범위를 벗어납니다.  
  
### <a name="configuring-distribution-at-the-publisher"></a>게시자에서 배포 구성  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **배포 구성**을 클릭합니다.  
  
    > [!NOTE]  
    >  실제 서버 이름이 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localhost **를 사용하여** 에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 **'localhost'** 서버에 연결할 수 없다는 경고가 표시됩니다. 경고 대화 상자에서 **확인을** 클릭 합니다. **서버에 연결** 대화 상자에서 **서버 이름** 을 **localhost** 에서 실제 서버 이름으로 변경합니다. **연결**을 클릭합니다.  
  
     배포 구성 마법사가 시작됩니다.  
  
3.  **배포자** 페이지에서 **'**_ \< ServerName>_'이 ( **가) 자체 배포자 역할을 하도록 선택 합니다. 배포 데이터베이스와 로그를 만든 SQL Server** **다음을 클릭 합니다**.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행되고 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**에이전트 시작** 페이지에서 **예**를 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작되도록 구성합니다. **다음**을 클릭합니다.  
  
5.  **\\\\** \< **스냅숏 폴더** 텍스트 상자에 _Machine_Name>_ **\repldata** 를 입력 하 고 \< *Machine_Name>* 게시자의 이름을 입력 한 후 **다음**을 클릭 합니다.  
  
6.  마법사의 나머지 페이지에 기본값을 적용합니다.  
  
7.  **마침** 을 클릭하여 배포를 사용하도록 설정합니다.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>게시자에서 데이터베이스 권한 설정  
  
1.  에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **보안**을 확장 하 고 **로그인**을 마우스 오른쪽 단추로 클릭 한 다음 **새 로그인**을 선택 합니다.  
  
2.  **일반** 페이지에서 **검색**을 클릭하고 **선택할 개체 이름 입력** 상자에 \<_Machine_Name>_**\repl_snapshot**을 입력한 다음 **이름 확인**, **확인**을 차례로 클릭합니다. 여기서 \<*Machine_Name>* 은 로컬 게시자 서버의 이름입니다.  
  
3.  **사용자 매핑** 페이지의 **이 로그인으로 매핑된 사용자** 목록에서 **배포** 및 데이터베이스를 모두 선택 합니다 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
     **데이터베이스 역할 멤버 자격** 목록에서 `db_owner` 두 데이터베이스의 로그인에 대 한 역할을 선택 합니다.  
  
4.  **확인** 을 클릭하여 로그인을 만듭니다.  
  
5.  1-4단계를 반복하여 로컬 repl_logreader 계정에 대한 로그인을 만듭니다. 이 로그인은 `db_owner` **배포** 및 **AdventureWorks** 데이터베이스에서 고정 데이터베이스 역할의 멤버인 사용자 에게도 매핑되어야 합니다.  
  
6.  1-4단계를 반복하여 로컬 repl_distribution 계정에 대한 로그인을 만듭니다. 이 로그인은 `db_owner` **배포** 데이터베이스에서 고정 데이터베이스 역할의 멤버인 사용자에 게 매핑되어야 합니다.  
  
7.  1-4단계를 반복하여 로컬 repl_merge 계정에 대한 로그인을 만듭니다. 이 로그인에는 **배포** 와 **AdventureWorks** 데이터베이스의 사용자 매핑이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](configure-distribution.md)   
 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)  
  
  
