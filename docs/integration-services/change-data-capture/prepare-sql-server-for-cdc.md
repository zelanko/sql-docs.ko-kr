---
title: "SQL Server CDC를 위한 준비 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29eee5c85a323e70dab3ac9bdb25bd72820b0489
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="prepare-sql-server-for-cdc"></a>CDC를 위한 SQL Server 준비
  Oracle CDC Service에서는 모든 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 MSXDBCDC 데이터베이스가 포함되어야 합니다. CDC Service 구성 콘솔에서 SQL Server 준비 작업을 사용하여 이 데이터베이스를 만듭니다. 이 작업은 이 데이터베이스의 필수 테이블, 저장 프로시저 및 기타 필수 아티팩트를 만들기 위해 실행되는 특수 스크립트를 만듭니다. 이 작업은 각 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 한 번만 수행됩니다.  
  
 MSXDBCDC 데이터베이스에 대한 자세한 내용은 MSXDBCDC 데이터베이스를 참조하십시오.  
  
 CDC Service 구성 콘솔에서 **SQL Server 준비**를 클릭합니다. 이 옵션을 사용할 수 없는 경우 콘솔의 왼쪽 창에서 **로컬 CDC Service** 가 선택되어 있는지 확인합니다.  
  
## <a name="options"></a>옵션  
  
### <a name="server-name"></a>서버 이름  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 있는 서버의 이름을 입력합니다.  
  
### <a name="authentication"></a>인증  
 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**  
  
-   **SQL Server 인증**: 이 옵션을 선택하는 경우 연결 중인 **에서 사용자의** 사용자 이름 **및** 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력해야 합니다.  
  
 Oracle CDC에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하려면 로그인은 MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있어야 합니다. MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있는 로그인(예: `sysasmin` 역할의 멤버)의 자격 증명을 입력합니다.  
  
### <a name="options"></a>옵션  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
-   **연결 제한 시간**: 제한 시간이 초과되기 전에 Oracle용 CDC Service가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
-   **실행 제한 시간**: 제한 시간이 초과되기 전에 Oracle CDC Windows 서비스에서 명령이 실행될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
-   **연결 암호화**: 암호화된 연결을 사용하는 대상 **인스턴스와 Oracle CDC Service 사이의 통신을 위해** 연결 암호화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택합니다.  
  
-   **고급**: 필요한 경우 모든 추가 연결 속성을 입력합니다.  
  
### <a name="view-script"></a>스크립트 보기  
 설치 스크립트의 읽기 전용 버전을 보려면 **스크립트 보기** 를 클릭합니다. 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자는 이 스크립트를 SQL Server 관리 콘솔에 복사하여 편집할 수 있습니다. SQL Server 스크립트 준비에 대한 자세한 내용은 [Oracle CDC를 위한 SQL Server 준비-스크립트 보기](../../integration-services/change-data-capture/prepare-sql-server-for-oracle-cdc-view-script.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [CDC Service에서 작업 하는 방법](../../integration-services/change-data-capture/how-to-work-with-cdc-services.md)   
 [CDC를 위한 SQL Server를 준비 하는 방법](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
