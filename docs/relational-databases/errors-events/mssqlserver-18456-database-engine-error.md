---
title: MSSQLSERVER_18456 | Microsoft 문서
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
ms.assetid: c417631d-be1f-42e0-8844-9f92c77e11f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ab33fa19b968990e81851edac9d91fb55db81049
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "77146314"
---
# <a name="mssqlserver_18456"></a>MSSQLSERVER_18456
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18456|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOGON_FAILED|  
|메시지 텍스트|사용자 '%.*ls'이(가) 로그인하지 못했습니다.%.\*ls|  
  
## <a name="explanation"></a>설명  
잘못된 암호나 사용자 이름과 관련된 인증 실패로 인해 연결 시도가 거부되면 다음과 유사한 메시지가 클라이언트로 반환됩니다.  "사용자 '<user_name>'이(가) 로그인하지 못했습니다. (Microsoft SQL Server, 오류: 18456)".  
  
클라이언트로 반환되는 추가 정보는 다음과 같습니다.  
  
"사용자 '<user_name>'이(가) 로그인하지 못했습니다. (.Net SqlClient 데이터 공급자)"  
  
-----------------------------\-  
  
"서버 이름: <computer_name>"  
  
"오류 번호: 18456"  
  
"심각도: 14"  
  
"상태: 1"  
  
"줄 번호: 65536"  
  
다음 메시지가 반환될 수도 있습니다.  
  
"메시지 18456, 수준 14, 상태 1, 서버 <computer_name>, 줄 1"  
  
"사용자 '<user_name>'이(가) 로그인하지 못했습니다."  
  
## <a name="additional-error-information"></a>추가 오류 정보  
보안 향상을 위해 클라이언트로 반환되는 오류 메시지는 의도적으로 인증 오류의 특성을 숨깁니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그의 해당 오류에는 인증 실패 조건에 매핑되는 오류 상태가 포함되어 있습니다. 로그인 실패 이유를 확인하려면 오류 상태를 다음 목록과 비교합니다.  
  
|시스템 상태|Description|  
|---------|---------------|  
|1|오류 정보를 사용할 수 없습니다. 일반적으로 이 상태는 오류 정보를 수신할 수 있는 권한이 없음을 의미합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자에게 문의하십시오.|  
|2|사용자 ID가 잘못되었습니다.|  
|5|사용자 ID가 잘못되었습니다.|  
|6|SQL Server 인증에 Windows 로그인 이름을 사용하려고 했습니다.|  
|7|로그인을 사용할 수 없으며 암호가 잘못되었습니다.|  
|8|암호가 잘못되었습니다.|  
|9|암호가 잘못되었습니다.|  
|11|올바른 로그인이지만 서버 액세스에 실패했습니다. 예를 들어 Windows 사용자에게 로컬 Administrators 그룹의 멤버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 액세스할 수 있는 권한이 있지만 Windows에서 관리자 자격 증명을 제공하지 않는 경우에 이 오류가 발생할 수 있습니다. 연결하려면 **관리자 권한으로 실행** 옵션을 사용하여 연결 프로그램을 시작하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 특정 로그인으로 Windows 사용자를 추가합니다.|  
|12|올바른 로그인이지만 서버 액세스에 실패했습니다.|  
|18|암호를 변경해야 합니다.|  
|38, 46|사용자가 요청한 데이터베이스를 찾을 수 없습니다.|
|58| SQL Server가 Windows 인증만 사용하도록 설정되고 클라이언트가 SQL 인증을 사용하여 로그인을 시도하는 경우입니다. 또 다른 원인은 SID가 일치하지 않는 경우입니다.|
|102 - 111|AAD 오류입니다.|
|122 - 124|빈 사용자 이름 또는 암호로 인한 오류입니다.|
|126|사용자가 요청한 데이터베이스가 없습니다.|
|132 - 133|AAD 오류입니다.|
  
다른 오류 상태가 있으며 예기치 않은 내부 처리 오류를 나타냅니다.  
  
**일반적이진 않지만 가능한 다른 원인**  
  
다음과 같은 상황에서 **SQL Server 인증을 사용하여 로그인하지 못했습니다. 서버가 Windows 인증만 사용하도록 구성되어 있습니다.** 오류 원인이 반환할 수 있습니다.  
  
-   서버가 혼합 모드 인증으로 구성되고, ODBC 연결이 TCP 프로토콜을 사용하고, 신뢰할 수 있는 연결을 사용해야 한다고 연결에 명시적으로 지정되어 있지 않은 경우  
  
-   서버가 혼합 모드 인증으로 구성되고, ODBC 연결이 명명된 파이프를 사용하고, 클라이언트가 명명된 파이프를 여는 데 사용한 자격 증명이 자동으로 사용자를 가장하는 데 사용되고, 신뢰할 수 있는 연결을 사용해야 한다고 연결에 명시적으로 지정되어 있지 않은 경우  
  
이 문제를 해결하려면 연결 문자열에 **TRUSTED_CONNECTION = TRUE**를 포함합니다.  
  
## <a name="examples"></a>예  
이 예에서 인증 오류 상태는 8이며 암호가 잘못되었음을 나타냅니다.  
  
|Date|원본|메시지|  
|--------|----------|-----------|  
|2007-12-05 20:12:56.34|로그온|오류: 18456, 심각도: 14, 상태: 8.|  
|2007-12-05 20:12:56.34|로그온|사용자 '<user_name>'이(가) 로그인하지 못했습니다. [클라이언트: <ip address>]|  
  
> [!NOTE]  
> Windows 인증 모드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하고 나중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 인증 모드로 변경하면 처음에는 **sa** 로그인을 사용할 수 없습니다. 이 경우 상태 7 오류: "사용자 'sa'이(가) 로그인하지 못했습니다"가 발생합니다. **sa** 로그인을 사용하도록 설정하려면 [서버 인증 모드 변경](~/database-engine/configure-windows/change-server-authentication-mode.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려고 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 혼합 인증 모드로 구성되어 있는지 확인합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려고 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 있고 이 로그인 이름의 철자가 올바른지 확인합니다.  
  
Windows 인증을 사용하여 연결하려고 하는 경우 올바른 도메인에 제대로 로그인되어 있는지 확인합니다.  
  
오류 상태가 1일 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자에게 문의합니다.  
  
관리자 자격 증명을 사용하여 연결하려면 **관리자 권한으로 실행** 옵션을 사용하여 애플리케이션을 시작합니다. 연결되면 Windows 사용자를 개별 로그인으로 추가합니다.  
  
[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 포함된 데이터베이스를 지원하는 경우 포함된 데이터베이스 사용자로 마이그레이션한 후 해당 로그인이 삭제되지 않았는지 확인하십시오.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로컬로 연결하는 경우 **NT AUTHORITY\NETWORK SERVICE**에서 실행되는 서비스의 연결도 컴퓨터의 정규화된 도메인 이름을 사용하여 인증해야 합니다. 자세한 내용은 [방법: 네트워크 서비스 계정을 사용하여 ASP.NET의 리소스에 액세스](https://msdn.microsoft.com/library/ff647402.aspx)를 참조하십시오.  
  
