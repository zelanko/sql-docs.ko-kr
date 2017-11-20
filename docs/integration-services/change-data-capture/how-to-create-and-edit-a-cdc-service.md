---
title: "CDC Service 만들기 및 편집 하는 방법 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: daf64f88220832573485701883921ad575e789bc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-create-and-edit-a-cdc-service"></a>CDC Service를 만들고 편집하는 방법
  이 프로시저에서는 CDC Service 구성 콘솔에서 새 Oracle CDC Service를 만들고 편집하는 방법을 설명합니다.  
  
 이 프로시저는 Oracle CDC Service가 구성된 컴퓨터에서 관리자 권한이 있는 Windows 사용자가 수행해야 합니다.  
  
### <a name="to-create-a-new-cdc-service"></a>새 CDC Service를 만들려면  
  
1.  **시작** 메뉴에서 **Oracle용 CDC Service 구성**을 선택합니다.  
  
2.  왼쪽 창에서 로컬 CDC Service를 마우스 오른쪽 단추로 클릭하고 새 서비스를 선택합니다.  
  
     **동작** 창에서 **새 서비스** 를 클릭할 수도 있습니다.  
  
3.  새 Oracle CDC Service 대화 상자에서 필요한 정보를 입력합니다. 새 Oracle CDC Service 대화 상자에서 정보를 입력하는 방법은 [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) 을 참조하십시오.  
  
     새 Oracle CDC Service 대화 상자에서 제공하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 서비스를 실행할 때 Oracle CDC Service에서 사용됩니다. 이 로그인은 공용 고정 서버 역할의 구성원이면 가능하며 다른 권한은 필요 없습니다. 새 Oracle CDC 인스턴스를 추가하면 해당 로그인은 연결된 **CDC 데이터베이스에 대한** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 권한을 받게 됩니다.  
  
4.  필요한 정보를 다 입력한 후 **확인**을 클릭합니다.  
  
     Oracle CDC Windows 서비스 정의를 만들려면 프로그램은 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스에 대한 액세스 권한을 업데이트해야 합니다. **확인**을 클릭하면 사용자가 MSXDBCDC 데이터베이스의 업데이트 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력할 수 있는 대화 상자가 나타납니다.  
  
     SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)을 참조하십시오.  
  
5.  **확인** 을 클릭하여 새 Oracle CDC Service 대화 상자를 닫습니다.  
  
### <a name="to-edit-a-cdc-service"></a>CDC Service를 편집하려면  
  
1.  **시작** 메뉴에서 **Oracle용 CDC Service 구성**을 선택합니다.  
  
2.  왼쪽 창에서 **로컬 CDC Service** 를 선택한 다음 편집하려는 로컬 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     중간에서 작업할 서비스를 선택하고 **동작** 창에서 **속성**을 선택할 수도 있습니다.  
  
3.  CDC Service 속성 대화 상자에서 필요한 정보를 입력합니다. CDC Service 속성 대화 상자에서 정보를 입력하는 방법은 [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) 을 참조하십시오.  
  
4.  필요한 정보를 다 입력한 후 **확인**을 클릭하면 SQL Server에 연결 대화 상자가 열립니다.  
  
     MSXDBCDC 데이터베이스에 대해 쓰기 권한이 없는 로그인이 새 Oracle CDC 인스턴스를 만들려고 시도하면 오류 메시지가 표시됩니다. 해당 대화 상자에서 **확인** 을 클릭하여 SQL Server에 연결 대화 상자를 표시합니다. 이 대화 상자에서 **db_owner** 데이터베이스 역할과 같은 MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있는 로그인의 자격 증명을 입력해야 합니다.  
  
     SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)을 참조하십시오.  
  
5.  Oracle에 연결 대화 상자에서 **확인** 을 클릭합니다. 두 대화 상자가 모두 닫히며 서비스가 업데이트되고 등록됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [변경 데이터 캡처 Designer for Oracle by Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC Service 만들기 및 편집](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)  
  
  

