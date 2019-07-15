---
title: 중앙 관리 서버 및 서버 그룹 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- configuration server
ms.assetid: da265482-3953-440a-ac23-0ab7e42a55eb
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: d9615fbb295ec6499c1743438b086abfc57b6bee
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681390"
---
# <a name="create-a-central-management-server-and-server-group"></a>중앙 관리 서버 및 서버 그룹 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]인스턴스를 중앙 관리 서버로 지정하는 방법에 대해 설명합니다. 중앙 관리 서버는 하나 이상의 중앙 관리 서버 그룹으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스 목록을 저장합니다. 중앙 관리 서버 그룹을 사용하여 수행되는 동작은 서버 그룹의 모든 서버에 적용됩니다. 여기에는 개체 탐색기를 사용하여 서버에 연결하는 동작 및 여러 서버에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 정책 기반 관리 정책을 동시에 실행하는 동작이 포함됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전은 중앙 관리 서버로 지정할 수 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **중앙 관리 서버 및 서버 그룹을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 msdb 데이터베이스의 두 데이터베이스 역할을 통해 중앙 관리 서버에 대한 액세스 권한을 부여합니다. 이 중 ServerGroupAdministratorRole 역할의 멤버만 중앙 관리 서버를 관리할 수 있으며 중앙 관리 서버에 연결하려면 ServerGroupReaderRole 역할의 멤버 자격이 필요합니다.  
  
 중앙 관리 서버에서 유지 관리하는 연결은 Windows 인증을 사용하여 사용자 컨텍스트 내에서 실행되므로 등록된 서버에 대한 유효 사용 권한은 달라질 수 있습니다. 예를 들어 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A 인스턴스에서는 sysadmin 고정 서버 역할의 멤버이지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B 인스턴스에서는 제한된 사용 권한을 가질 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 절차에서는 다음 단계를 수행하는 방법에 대해 설명합니다.  
  
1.  중앙 관리 서버를 만듭니다.  
  
2.  중앙 관리 서버에 하나 이상의 서버 그룹을 추가하고 서버 그룹에 하나 이상의 등록된 서버를 추가합니다.  
  
#### <a name="create-a-central-management-server"></a>중앙 관리 서버 만들기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
2.  등록된 서버에서 **데이터베이스 엔진**을 확장하고 **중앙 관리 서버**를 마우스 오른쪽 단추로 클릭한 다음 **중앙 관리 서버 등록**을 클릭합니다.  
  
3.  **새 서버 등록[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대화 상자의 서버 드롭다운 목록에서 중앙 관리 서버로 만들**  인스턴스를 선택합니다. 중앙 관리 서버를 만들려면 Windows 인증을 사용해야 합니다.  
  
4.  **등록된 서버**에서 서버 이름과 설명(선택 사항)을 입력합니다.  
  
5.  **연결 속성** 탭에서 네트워크 및 연결 속성을 검토하거나 수정합니다. 자세한 내용은 [서버에 연결&#40;연결 속성 페이지&#41; 데이터베이스 엔진](https://msdn.microsoft.com/library/edc1143c-6a47-4b02-92ab-441bdea8ea8a)을 참조하세요.  
  
6.  **테스트**를 클릭하여 연결을 테스트합니다.  
  
7.  **저장**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 중앙 관리 서버 **폴더 아래에** 인스턴스가 표시됩니다.  
  
#### <a name="create-a-new-server-group-and-add-servers-to-the-group"></a>새 서버 그룹을 만들고 그룹에 서버 추가  
  
1.  **등록된 서버**에서 **중앙 관리 서버**를 확장합니다. 위 절차에서 추가한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 서버 그룹**을 선택합니다.  
  
2.  **새 서버 그룹 속성**에서 그룹 이름과 설명(선택 사항)을 입력합니다.  
  
3.  **등록된 서버**에서 서버 그룹을 마우스 오른쪽 단추로 클릭하고 **새 서버 등록**을 클릭합니다.  
  
4.  새 서버 등록에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택합니다. 자세한 내용은 [새 등록된 서버 만들기&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)를 참조하세요. 필요에 따라 서버를 더 추가합니다.  
  
#### <a name="to-execute-queries-against-several-configuration-targets-at-the-same-time"></a>여러 구성 대상에 대해 동시에 쿼리를 실행하려면  
  
-   하나의 중앙 관리 서버, 하나 이상의 서버 그룹 및 하나 이상의 등록된 서버를 만든 후에는 전체 그룹에 대해 동시에 쿼리를 실행할 수 있습니다. 서버 그룹의 서버에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 동시에 실행하는 방법에 대한 자세한 내용은 [여러 서버에 대해 동시에 문 실행&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [중앙 관리 서버를 사용하여 여러 서버 관리](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
