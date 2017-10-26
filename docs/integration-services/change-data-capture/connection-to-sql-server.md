---
title: "SQL Server에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f2c0ec017651177fe6bb78d7aef5df35a27b5b6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connection-to-sql-server"></a>SQL 서버에 연결
  MSXDBCDC 데이터베이스에 대해 쓰기 권한이 포함된 데이터베이스 역할(예: **db_owner** 역할)이 없는 로그인이 Oracle CDC 인스턴스를 만들려고 시도하면 SQL Server에 연결 대화 상자가 표시됩니다.  
  
 이 대화 상자에서 **db_owner** 데이터베이스 역할과 같이 MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있는 로그인의 자격 증명을 입력하여 새 Oracle CDC 인스턴스를 만들어야 합니다.  
  
 SQL Server에 연결 대화 상자에 다음 정보를 입력합니다.  
  
### <a name="server-name"></a>서버 이름  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 있는 서버의 이름을 입력합니다.  
  
### <a name="authentication"></a>인증  
 다음 중 하나를 선택합니다.  
  
-   Windows 인증  
  
-   **SQL Server 인증**: 이 옵션을 선택하는 경우 연결 중인 **에서 사용자의** 로그인 **및** 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력해야 합니다.  
  
### <a name="options"></a>옵션  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
-   **연결 제한 시간**: 시간 초과 오류가 발생하기 전에 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
-   **실행 제한 시간**: 시간 초과 오류가 발생하기 전에 프로그램이 SQL 명령 실행을 마칠 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
-   **연결 암호화**: 설정 중인 **연결을 암호화하여 개인 정보를 보호하려면** 연결 암호화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택합니다.  
  
-   **고급**: **고급** 을 클릭하고 필요한 경우 고급 연결 속성 대화 상자에 추가 연결 속성을 입력합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 연결 CDC Service에 필요한 권한](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  

