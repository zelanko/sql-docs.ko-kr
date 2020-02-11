---
title: 여러 서버에 대해 동시에 문 실행
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 55b77ddf4284dc4f06e8036d0ae1b0c86b3544f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244639"
---
# <a name="execute-statements-against-multiple-servers-simultaneously-sql-server-management-studio"></a>여러 서버에 대해 동시에 문 실행(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 로컬 서버 그룹 또는 중앙 관리 서버와 하나 이상의 서버 그룹 및 그룹 내의 하나 이상의 등록된 서버를 만든 다음 전체 그룹을 쿼리하여 여러 서버를 동시에 쿼리하는 방법에 대해 설명합니다. 쿼리에서 반환되는 결과는 단일 결과 창으로 결합되거나 별도의 결과 창에 반환될 수 있습니다. 결과 집합에는 각 서버에 대한 쿼리에서 사용하는 서버 이름 및 로그인에 대한 추가 열이 포함되어 있습니다. 중앙 관리 서버와 하위 서버는 Windows 인증을 사용해서만 등록할 수 있습니다. Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 로컬 서버 그룹의 서버를 등록할 수 있습니다.  
  
> [!NOTE]  
>  다음 절차를 실행하기 전에 중앙 관리 서버 및 서버 그룹을 만듭니다. 자세한 내용은 [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](create-a-central-management-server-and-server-group.md)를 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **여러 서버에 대해 문을 실행하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 중앙 관리 서버에서 유지 관리하는 연결은 Windows 인증을 사용하여 사용자 컨텍스트에서 실행되기 때문에 등록된 서버에 대한 유효 사용 권한이 달라질 수 있습니다. 예를 들어 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A 인스턴스에서는 sysadmin 고정 서버 역할의 멤버이지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B 인스턴스에서는 제한된 사용 권한을 가질 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-execute-statements-against-multiple-configuration-targets-simultaneously"></a>여러 구성 대상에 대해 동시에 문을 실행하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
2.  중앙 관리 서버를 확장하고 서버 그룹을 마우스 오른쪽 단추로 클릭하고 **연결**을 가리킨 다음 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 편집기에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력하고 실행합니다.  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     기본적으로 결과 창이 서버 그룹에 있는 모든 서버의 쿼리 결과를 결합합니다.  
  
#### <a name="to-change-the-multiserver-results-options"></a>다중 서버 결과 옵션을 변경하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **쿼리 결과**를 확장하고 **SQL Server**를 확장한 다음 **다중 서버 결과**를 클릭합니다.  
  
3.  **다중 서버 결과** 페이지에서 원하는 옵션 설정을 지정한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중앙 관리 서버를 사용하여 여러 서버 관리](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
