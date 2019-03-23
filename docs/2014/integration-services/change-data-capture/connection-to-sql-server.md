---
title: SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d597cb7776362c44ca53e8d544f66608d8d37c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377201"
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
  
-   **SQL Server 인증**: 이 옵션을 선택 하는 경우 입력 해야 합니다 **로그인** 및 **암호** 사용자에 대 한는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 하는 합니다.  
  
### <a name="options"></a>변수  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
-   **연결 제한 시간**: 제한 시간 초과 오류가 발생하기 전에 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
-   **실행 제한 시간**: 제한 시간 초과 오류가 발생하기 전에 프로그램이 SQL 명령 실행을 마칠 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
-   **연결 암호화**: 선택 **연결 암호화** 되도록는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 되 고 개인 정보 보호를 보장 하기 위해 암호화 된 연결입니다.  
  
-   **고급**: **고급** 을 클릭하고 필요한 경우 고급 연결 속성 대화 상자에 추가 연결 속성을 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 연결 CDC Service에 필요한 권한](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
