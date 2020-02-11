---
title: MSSQLSERVER 속성에 대한 프로토콜(고급 탭) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9000dd2b7456036f4828640694aaf697036b71d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62645796"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER 속성에 대한 프로토콜(고급 탭)
  
  **MSSQLSERVER에 대한 프로토콜 속성** 대화 상자의 **고급** 탭을 사용하여 **** 에 대해 인증에 대한 확장된 보호[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 구성할 수 있습니다. **확장 된 보호** 는 운영 체제에서 구현 하는 네트워크 구성 요소의 기능입니다. **확장 된 보호** 는 windows 7 및 windows Server 2008 r 2에서 사용할 수 있으며 이전 운영 체제의 서비스 팩에 포함 되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**확장 된 보호**를 사용 하 여 연결 하면의 보안이 강화 됩니다. 
  **확장된 보호** 기능의 이점을 활용하려면 **플래그** 탭에서 **암호화 적용** 을 선택해야 합니다.  
  
> [!IMPORTANT]  
>  Windows에서는 기본적으로 **확장된 보호** 를 사용할 수 없습니다. Windows에서 **확장된 보호** 를 사용하는 방법은 기술 자료 문서 [인증에 대한 확장된 보호](https://go.microsoft.com/fwlink/?LinkId=178431)를 참조하십시오.  
  
 기타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 구성하는 방법과 **확장된 보호**에 대한 전체 설명을 보려면 [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752)의 최신 정보를 참조하십시오.  
  
 **확장 된 보호** 는부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 완벽 하 게 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]지원 됩니다. 다른 ** 개의 클라이언트 제공 업체를위한 **개의 확장 된 보호[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 지원은 현재 지원되지 않습니다.  
  
## <a name="options"></a>옵션  
 **확장 된 보호**  
 세 가지 값을 사용할 수 있습니다.  
  
-   
  **해제**로 설정하면 **확장된 보호** 를 사용할 수 없습니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 클라이언트 보호 여부에 관계없이 모든 클라이언트로부터의 연결을 허용합니다. **Off** 는 이전 및 패치가 적용 되지 않은 운영 체제와 호환 되지만 안전성은 떨어집니다. 클라이언트 운영 체제에서 확장된 보호를 지원하지 않는 경우에만 이 설정을 사용하십시오.  
  
-   
  **허용**으로 설정하면 **확장된 보호** 를 지원하는 운영 체제로부터의 연결에 대해 **확장된 보호**를 사용해야 합니다. 보호된 클라이언트 운영 체제에서 실행되는 보호되지 않는 클라이언트 애플리케이션으로부터의 연결은 거부됩니다. 보호 되지 않는 운영 체제 로부터의 연결에 대해서는 **확장 된 보호** 를 무시 합니다. 이 설정은 **해제**보다는 안전하지만 가장 안전한 설정은 아닙니다. 
  **확장된 보호** 를 지원하는 운영 체제 또는 애플리케이션과 지원하지 않은 운영 체제 또는 애플리케이션이 혼합되어 있는 환경에서는 이 설정을 사용하십시오.  
  
-   
  **필수**로 설정하면 보호된 운영 체제에서 실행되는 보호된 애플리케이션으로부터의 연결만 허용됩니다. 이 설정은 세 가지 옵션 중 가장 안전하지만, **확장된 보호** 를 지원하지 않는 운영 체제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다.  
  
 **허용 되는 NTLM Spn**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 여러 NTLM SPN(서비스 사용자 이름)으로 식별되는 경우 SPN이 세미콜론으로 구분되는 일련의 문자열로 나열됩니다. 예를 들어 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**값은 이름이 **MSSQLSvc/HOST1.Contoso.com** 및 **MSSQLSvc/HOST2.Contoso.com** 인 SPN에 대한 클라이언트의 연결이 허용됨을 나타냅니다. 변수의 최대 길이는 2048자입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 인증에 대한 확장된 보호](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
