---
title: 인스턴스를 만들기 위한 SQL Server 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e0f879d566608f38a99d9fb4a316b0284213403
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816836"
---
# <a name="sql-server-connection-for-instance-creation"></a>인스턴스를 만들기 위한 SQL Server 연결
  Oracle CDC 인스턴스를 만드는 첫 번째 단계 중 하나는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 CDC 데이터베이스를 만드는 것입니다. 이 CDC 데이터베이스가 SQL Server CDC에 사용되며 이를 위해서는 `sysadmin` 고정 서버 역할의 멤버인 로그인이 필요합니다.  
  
 **Oracle CDC 인스턴스 만들기** 마법사를 시작하는 사용자가 `sysadmin` 고정 서버 역할의 멤버가 아닌 경우 **SQL Server에 연결** 대화 상자가 열리고 SQL Server CDC에 데이터베이스 사용 태스크를 수행하기 위한 `sysadmin` 역할의 멤버에 대해 자격 증명을 요청합니다. CDC 데이터베이스가 만들어지면 `sysadmin` 로그인은 삭제되고 Oracle Designer 콘솔 시작 시 사용된 원래 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 작업이 다시 시작됩니다.  
  
## <a name="task-list"></a>작업 목록  
 **SQL Server에 연결** 대화 상자에 다음 정보를 입력합니다.  
  
 **서버 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 있는 서버의 이름을 입력합니다.  
  
 **인증**  
 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**  
  
-   **SQL Server 인증**: 이 옵션을 선택하는 경우 연결 중인 **에서 사용자의** 로그인 **및** 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력해야 합니다.  
  
 MSXCDCDB 데이터베이스에 대한 액세스를 허용하는 데이터베이스 역할이 로그인에 있어야 합니다. 사용 중인 모든 추가 데이터베이스에 대한 액세스 권한도 있는 것이 좋습니다. 그렇지 않으면 사용자가 해당 데이터베이스의 데이터를 볼 수 없습니다.  
  
 **옵션**  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
-   **연결 제한 시간**: 제한 시간이 초과되기 전에 Oracle용 CDC Service가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
-   **실행 제한 시간**: 제한 시간이 초과되기 전에 Oracle CDC Windows 서비스에서 명령이 실행될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
-   **연결 암호화**: 암호화된 연결을 사용하는 대상 **인스턴스와 Oracle CDC Service 사이의 통신을 위해** 연결 암호화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택합니다.  
  
-   **고급**: **고급** 을 클릭하고 필요한 경우 고급 연결 속성 대화 상자에 추가 연결 속성을 입력합니다.  
  
     고급 연결 속성 대화 상자에 대한 자세한 내용은 [Advanced Connection Properties](../../integration-services/change-data-capture/advanced-connection-properties.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 변경 데이터베이스 만들기](../../integration-services/change-data-capture/create-the-sql-server-change-database.md)   
 [SQL Server 연결을 위해 CDC Designer에 대해 필요한 권한](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
