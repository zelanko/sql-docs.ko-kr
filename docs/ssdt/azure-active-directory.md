---
title: "SSDT(SQL Server Data Tools)의 Azure Active Directory 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/05/2018
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssdt
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 14a6ae78a0ed5969ce3ab65dbd09b81680076fdb
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)의 Azure Active Directory 지원

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

SSDT(SQL Server Data Tools)는 여러 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) 인증 방법을 제공합니다.

![SSDT 연결 대화 상자](media/azure-active-directory/interactive.png)

## <a name="active-directory-password-authentication"></a>Active Directory 암호 인증

Active Directory 암호 인증은 Azure AD(Azure Active Directory)의 ID를 사용하여 Azure SQL Database에 연결하는 메커니즘입니다.  Azure로 페더레이션되지 않은 도메인에서 자격 증명을 사용하여 Windows에 로그인하는 경우 또는 초기 도메인이나 클라이언트 도메인에 따라 Azure AD를 사용하는 Azure AD 인증을 사용하는 경우 이 방법으로 연결합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL 데이터베이스에 연결](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)을 참조하세요.  

## <a name="active-directory-integrated-authentication"></a>Active Directory 통합 인증

Active Directory 통합 인증은 Azure AD(Azure Active Directory)의 ID를 사용하여 Azure SQL Database에 연결하는 메커니즘입니다. 페더레이션된 도메인에서 Azure Active Directory 자격 증명을 사용하여 Windows에 로그인하는 경우 이 방법으로 연결합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL 데이터베이스에 연결](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)을 참조하세요.

## <a name="active-directory-interactive-authentication-preview"></a>Active Directory 대화형 인증(미리 보기)

SSDT는 Azure SQL 데이터베이스에 연결하기 위한 새로운 인증 방법인 **Active Directory 대화형 인증**을 제공합니다.


> [!NOTE]
> Active Directory 대화형 인증은 [Visual Studio 2017 미리 보기](https://www.visualstudio.com/vs/preview/)에서 SSDT와 연결할 때 사용할 수 있으며 [.NET 4.7.2 미리 보기(KB4038188)](https://go.microsoft.com/fwlink/?linkid=867317)가 SSDT를 실행하는 컴퓨터에 설치되어 있어야 합니다. .NET 4.7.2 미리 보기(KB4038188)가 설치되어 있지 않으면 Active Directory 대화형 인증 옵션을 사용할 수 없습니다.


Active Directory 대화형 인증은 AD(Azure Active Directory) MFA(Multi-Factor Authentication)를 사용하여 Azure SQL Database에 인증할 수 있도록 대화형 인증을 지원합니다. 이 방법은 네이티브 및 페더레이션 Azure AD 사용자와 다른 계정의 게스트 사용자를 지원합니다(B2B 사용자, @outlook.com, @hotmail.com, @live.com 및 @gmail.com과 같은 Microsoft 및 타사 계정 포함). 이 방법을 지정하면 **사용자 이름**을 지정해야 하며 [암호] 필드는 사용하지 않도록 설정됩니다. 

‘Active Directory 대화형 인증’으로 인증할 경우 인증 창이 열리며 사용자가 이 창에 암호를 직접 입력해야 합니다.

![로그인 대화 상자](media/azure-active-directory/sign-in.png)

인증 과정 중 이 추가 MFA 팝업 창을 통해 Azure AD에서 MFA를 적용합니다.

> [!NOTE]
> ‘Active Directory 대화형 인증’의 경우 사용자가 암호를 직접 입력해야 하므로 자동 워크플로에는 사용하지 않는 것이 좋습니다.


## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항

- ‘Active Directory 대화형 인증’은 Azure SQL 데이터베이스에 연결할 때만 지원됩니다. 온-프레미스 또는 VM 상의 SQL Server나 Azure SQL Data Warehouse는 지원되지 않습니다.
- ‘Active Directory 대화형 인증’은 ‘서버 탐색기’의 연결 대화 상자에서 지원되지 않으며, ‘SQL Server 개체 탐색기’에서 SSDT를 사용하여 연결해야 합니다.
- 현재 로그인한 Visual Studio 계정을 사용한 Single Sign-On 통합은 SSDT에서 지원되지 않습니다.
- Visual Studio 설치 중 확장 디렉터리에 설치되는 SQLPackage.exe는 해당 위치에서 사용하기 위한 것은 아닙니다. AAD에 SQLpackage.exe를 사용하려면 https://www.microsoft.com/en-us/download/details.aspx?id=55088을 참조하세요. 
- 새 인증 방법을 비롯해 AAD 인증에서는 SSDT 데이터 비교가 지원되지 않습니다.  





## <a name="see-also"></a>참고 항목  
[다단계 인증](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[SQL Database에서 Azure Active Directory 인증 ](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[Visual Studio의 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](http://blogs.msdn.com/b/ssdt/)  
[DACFx API 참조](https://msdn.microsoft.com/library/dn645454.aspx)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  
