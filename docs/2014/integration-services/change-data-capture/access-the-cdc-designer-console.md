---
title: CDC Designer 콘솔 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: df4e9ffabcec2d484d4d747c1093082dca7855bf
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438960"
---
# <a name="access-the-cdc-designer-console"></a>CDC Designer 콘솔 액세스
  콘솔을 설치한 컴퓨터에서 CDC Designer 콘솔에 액세스할 수 있습니다. 설치에 대한 자세한 내용은 설치를 참조하십시오.  
  
 CDC Designer 콘솔을 열 때 SQL Server에 연결 대화 상자가 열립니다.  
  
 CDC Designer에 액세스하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 MSXDBCDC 데이터베이스에 대한 UPDATE 권한이 있어야 합니다. 또한 새 Oracle CDC 인스턴스를 만들려면 `dbcreator` 고정 서버 역할이어야 합니다. 사용 중인 CDC 데이터베이스에 대한 SELECT 권한도 로그인이 갖는 것이 좋습니다. 그렇지 않으면 사용자가 해당 데이터베이스의 상태를 볼 수 없습니다.  
  
 SQL Server에 연결 대화 상자에 다음 정보를 입력합니다.  
  
### <a name="server-name"></a>서버 이름  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 있는 서버의 이름을 입력합니다.  
  
### <a name="authentication"></a>인증  
 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**  
  
-   **SQL Server 인증**: 이 옵션을 선택하는 경우 연결 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자의 **로그인** 및 **암호**를 입력해야 합니다.  
  
 MSXCDCDB 데이터베이스에 대한 액세스를 허용하는 데이터베이스 역할이 로그인에 있어야 합니다. 사용 중인 모든 추가 데이터베이스에 대한 액세스 권한도 있는 것이 좋습니다. 그렇지 않으면 사용자가 해당 데이터베이스의 데이터를 볼 수 없습니다.  
  
### <a name="options"></a>옵션  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
 **연결 제한 시간**  
 제한 시간이 초과되기 전에 Oracle용 CDC Service가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
 **실행 제한 시간**  
 제한 시간이 초과되기 전에 Oracle CDC Windows 서비스에서 명령이 실행될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
 **연결 암호화**  
 암호화된 연결을 사용하는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 Oracle CDC Service 사이의 통신을 위해 **연결 암호화**를 선택합니다.**고급**: **고급** 을 클릭하고 필요한 경우 고급 연결 속성 대화 상자에 추가 연결 속성을 입력합니다.  
  
 **고급**  
 **고급** 을 클릭하고 필요한 경우 고급 연결 속성 대화 상자에 추가 연결 속성을 입력합니다.  
  
 고급 연결 속성 대화 상자에 대한 자세한 내용은 [Advanced Connection Properties](advanced-connection-properties.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 연결을 위해 CDC Designer에 대해 필요한 권한](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
