---
title: SSDT의 Azure Active Directory
description: SSDT(SQL Server Data Tools)에서 Azure SQL Database 및 Azure Synapse Analytics용으로 제공되는 Azure Active Directory 인증 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
author: markingmyname
ms.author: maghan
reviewer: ''
ms.custom: seo-lt-2019
ms.date: 10/28/2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 564e6ad8cc4ab7cc14d816b34e5332412f912739
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489733"
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)의 Azure Active Directory 지원

[!INCLUDE[appliesto-xx-asdb-asdb-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

SSDT(SQL Server Data Tools)는 여러 [Azure AD(Azure Active Directory)](/azure/active-directory/active-directory-whatis) 인증 방법을 제공합니다.

Visual Studio에서 **보기** 메뉴에서 **SQL Server 개체 탐색기** 를 열고 **SQL Server 추가** 를 선택합니다.

![SSDT 연결 대화 상자](media/azure-active-directory/interactive.png)

#### <a name="which-azure-sql-products"></a>Azure SQL 제품이란?

이 문서에서는 [Azure 클라우드](https://azure.microsoft.com/)에서 다음 *Azure SQL 제품* 목록에 대해 Azure AD를 설명합니다.

- Azure SQL Database
- Azure Synapse Analytics

## <a name="active-directory-password-authentication"></a>Active Directory 암호 인증

*Active Directory 암호 인증* 은 앞에 나열된 Azure SQL 제품에 연결하는 메커니즘입니다. 이 메커니즘은 Azure AD(Azure Active Directory)에서 ID를 사용합니다. 다음의 경우 이 연결 메서드를 사용합니다.

- Azure와 페더레이션되지 않은 도메인에서 자격 증명을 사용하여 Windows에 로그온합니다.
- Azure AD와 함께 Azure AD 인증을 사용합니다. 이는 초기 또는 클라이언트 도메인에 기반합니다.

자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/sql-database/sql-database-aad-authentication)을 참조하세요.  

## <a name="active-directory-integrated-authentication"></a>Active Directory 통합 인증

*Active Directory 통합 인증* 은 Azure AD(Azure Active Directory)에서 ID를 사용하여 나열된 Azure SQL 제품에 연결하는 메커니즘입니다. 페더레이션된 도메인에서 Azure Active Directory 자격 증명을 사용하여 Windows에 로그인하는 경우 이 방법으로 연결합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/sql-database/sql-database-aad-authentication)을 참조하세요.

## <a name="active-directory-interactive-authentication"></a>Active Directory 대화형 인증

*Active Directory 대화형 인증* 은 SSDT 그러나 [.NET Framework 4.7.2](/dotnet/api/?view=netframework-4.7.2&preserve-view=true) 이상 버전만 사용하여 나열된 Azure SQL 제품에 연결할 때 사용할 수 있습니다.

- [.NET Framework 모든 버전을 다운로드하고 설치합니다](https://www.microsoft.com/net/download/all).
- [Visual Studio 2017 버전 15.6](/visualstudio/releasenotes/vs2017-relnotes) 또는 이상 버전.

#### <a name="multi-factor-authentication-mfa"></a>MFA(Multi-Factor Authentication)

Active Directory 대화형 인증은 Azure AD(Active Directory) MFA(Multi-Factor Authentication)를 사용하여 나열된 Azure SQL 제품을 인증할 수 있도록 대화형 인증을 지원합니다. 이 메서드는 기본 및 페더레이션된 Azure AD 사용자 및 다른 계정의 게스트 사용자를 지원합니다. 다른 유형의 계정은 다음과 같습니다.

- B2B(Azure AD B2B) 사용자입니다.
- Microsoft 계정은 @outlook.com, @hotmail.com, @live.com 등과 같습니다.
- 타사 계정은 @gmail.com과 같습니다.

MFA 방법을 지정하면 **사용자 이름** 을 지정해야 하며 **암호** 필드는 사용하지 않도록 설정됩니다. 

#### <a name="password-entry"></a>암호 입력

‘Active Directory 대화형 인증’으로 인증할 경우 인증 창이 열리며 사용자가 이 창에 암호를 직접 입력해야 합니다.

![로그인 대화 상자](media/azure-active-directory/sign-in.png)

이 추가 MFA 팝업 창을 통해 Azure AD에서 MFA를 적용합니다.

> [!NOTE]
> 자동화된 워크플로는 *Active Directory 대화형 인증* 을 사용하여 차단됩니다. 수동으로 암호를 입력하는 형식으로 인증 프로세스와 상호 작용할 수 있는 사람이 있어야 합니다.

## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항

- *Active Directory 대화형 인증* 은 이 문서의 시작 부분에 나열된 Azure SQL 제품에 연결할 때만 지원됩니다. 온-프레미스 또는 VM 상의 SQL Server는 지원되지 않습니다.
- *Active Directory 대화형 인증* 은 *서버 탐색기* 의 연결 대화 상자에서는 지원되지 않습니다. *SQL Server 개체 탐색기* 로 SSDT를 사용하여 연결해야 합니다.
- 현재 로그인한 Visual Studio 계정을 사용한 Single Sign-On 통합은 SSDT에서 지원되지 않습니다.
- Visual Studio 설치 중 확장 디렉터리에 설치되는 SQLPackage.exe는 해당 위치에서 사용하기 위한 것은 아닙니다. Azure AD에서 SQLPackage.exe를 사용하려면 [데이터 계층 애플리케이션 프레임워크](https://www.microsoft.com/download/details.aspx?id=55088)로 이동하세요. 
- SSDT 데이터 비교는 Azure AD 인증에 대해 지원되지 않습니다.  


## <a name="see-also"></a>참고 항목  

[다단계 인증](/azure/sql-database/sql-database-ssms-mfa-authentication)  
[SQL Database에서 Azure Active Directory 인증 ](/azure/sql-database/sql-database-aad-authentication-configure)  
[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](/archive/blogs/ssdt/)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)
