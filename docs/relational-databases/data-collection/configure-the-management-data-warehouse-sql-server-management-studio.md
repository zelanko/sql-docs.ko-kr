---
title: "관리 데이터 웨어하우스 구성(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4165c8b8e8e11b281a31e04a3b0fd402146d4e71
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>관리 데이터 웨어하우스 구성(SQL Server Management Studio)
  이 항목에서는 데이터 수집기를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 단일 인스턴스 또는 여러 인스턴스에서 데이터 저장소를 지원하도록 관리 데이터 웨어하우스를 구성하는 방법에 대해 설명합니다. 이러한 인스턴스는 같은 서버에 있거나 다른 서버에 있을 수 있습니다. 그리고 [데이터 관리 웨어하우스 구성 마법사](#Wizard) 대화 상자의 사용자 인터페이스에 대해서도 설명합니다. 데이터 수집기 구성에 대한 자세한 내용은 [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시스템 서비스 계정(로컬 시스템, 네트워크 서비스 또는 로컬 서비스) 중 하나를 사용하여 실행되도록 구성되고 관리 데이터 웨어하우스는 데이터 수집기와 다른 인스턴스에서 생성될 경우 관리 데이터 웨어하우스에 데이터를 업로드하는 데 프록시를 사용하도록 컬렉션 집합을 구성해야 합니다.  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>다음 단일 인스턴스 또는 여러 인스턴스에서 관리 데이터 웨어하우스 구성: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중인지 확인합니다.  
  
2.  개체 탐색기에서 **관리** 노드를 확장합니다.  
  
3.  **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 확장하고 **관리 데이터 웨어하우스 구성**을 클릭합니다.  
  
4.  [관리 데이터 웨어하우스 구성 마법사](#Wizard) 를 사용하여 관리 데이터 웨어하우스를 만들고, 로그인을 구성하며, 데이터 컬렉션을 활성화하고, **시스템 데이터 컬렉션 집합**을 시작합니다.  
  
     여러 인스턴스를 구성하려면 5단계를 계속합니다.  
  
    > [!NOTE]  
    >  데이터 수집기가 동일한 관리 데이터 웨어하우스를 사용하는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치되어 있는 배포 환경에서 프록시를 사용하는 것이 최선의 방법입니다.  
  
5.  다른 인스턴스에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 다음 작업 중 하나를 수행합니다.  
  
    -   구성 관리 데이터 웨어하우스 마법사를 사용하여 기존 관리 데이터 웨어하우스의 데이터 컬렉션을 구성합니다.  
  
    -   **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **일반** 탭에서 기존 관리 데이터 웨어하우스와 이 관리 데이터 웨어하우스가 설치된 서버를 지정합니다.  
  
6.  데이터 수집기를 사용하는 데이터베이스 인스턴스가 모두 구성되어 공유 관리 데이터 웨어하우스에 데이터를 업로드할 때까지 5단계를 반복합니다.  
  
####  <a name="Wizard"></a> 관리 데이터 웨어하우스 구성 마법사  
 **시작 페이지**  
  
 시작 페이지는 데이터 컬렉션 구성 마법사의 첫 페이지입니다. 이 페이지의 표시 여부는 선택 사항입니다.  
  
 **이 시작 페이지를 다시 표시 안 함**  
 다음에 데이터 컬렉션 구성 마법사를 시작할 때 이 페이지를 표시하지 않으려면 선택합니다.  
  
 **관리 데이터 웨어하우스 저장소 구성 페이지**  
  
 이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 서버 및 관리 데이터 웨어하우스를 선택할 수 있습니다. 관리 데이터 웨어하우스는 수집된 데이터를 보관하는 관계형 데이터베이스입니다.  
  
> [!NOTE]  
>  서버에 관리 데이터 웨어하우스를 만들려면 적절한 수준의 권한이 있어야 합니다. 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요. 또한 관리 데이터 웨어하우스 역할에 대한 로그인을 만들려는 경우에도 적절한 수준의 권한이 있어야 합니다.  
  
 **서버 이름**  
 관리 데이터 웨어하우스를 호스팅할 서버의 이름을 지정합니다.  
  
 관리 데이터 웨어하우스를 구성할 때 **서버 이름** 은 항상 로컬 서버의 이름이며 수정할 수 없습니다.  
  
 **데이터베이스 이름**  
 수집된 데이터를 보관할 관계형 데이터베이스를 지정합니다. 목록을 사용하여 기존 데이터베이스를 선택하거나 **새로 만들기** 를 클릭하여 **새 데이터베이스** 대화 상자를 통해 새 데이터베이스를 만듭니다.  
  
 **새로 만들기** 옵션은 데이터 컬렉션 집합을 구성할 때만 사용할 수 있습니다.  
  
 **로그인 및 사용자 매핑 페이지**  
  
 이 페이지를 사용하여 관리 데이터 웨어하우스에 대한 데이터베이스 사용자 역할에 로그인을 매핑할 수 있습니다.  
  
 **이 로그인으로 매핑된 사용자**  
 관리 데이터 웨어하우스를 호스팅할 서버에 있는 기존 로그인을 표시합니다. 각 행에는 편집 가능한 **매핑** 확인란, **로그인** 이름 및 로그인 **유형** 이 들어 있습니다.  
  
 로그인에 대한 **매핑** 확인란을 선택하여 로그인을 지정합니다.  
  
 **데이터베이스 역할 멤버 자격:** *\<데이터 웨어하우스 이름>*  
 다음 중 하나 이상의 옵션 옆에 있는 확인란을 클릭하여 로그인이 매핑되는 관리 데이터 웨어하우스 역할을 선택합니다.  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **새 로그인**  
 **로그인 - 신규** 대화 상자를 열고 관리 데이터 웨어하우스에 대한 새 로그인을 만듭니다.  
  
 **마법사 완료 페이지**  
  
 이 페이지를 사용하여 데이터 컬렉션 구성을 확인하고 완료할 수 있습니다. 보기 창에 표시된 트리는 **마침**을 클릭할 때 적용되는 구성과 발생하는 동작을 보여 줍니다.  
  
 **데이터 컬렉션 구성 마법사 진행률 페이지**  
  
 이 페이지를 사용하여 각 구성 단계의 결과를 확인할 수 있습니다.  
  
 **세부 정보**  
 각 구성 단계를 **자세히** 표에서 행으로 표시합니다. 각 행에는 단계를 설명하는 **동작** 열과 단계의 성공 여부를 나타내는 **상태** 열이 포함됩니다. 오류가 있으면 **메시지** 열에 메시지가 표시됩니다.  
  
 **중지**  
 마법사 진행을 중지합니다.  
  
 **보고서**  
 데이터 컬렉션 구성에 대한 보고서를 표시합니다. 다음과 같은 보고서 옵션이 제공됩니다.  
  
-   보고서 보기  
  
-   보고서를 파일로 저장  
  
-   클립보드에 보고서 복사  
  
-   보고서를 전자 메일로 보내기  
  
 **닫기**  
 마법사를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_syscollector_enable_collector&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
