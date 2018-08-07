---
title: 전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4e6d6ac6fa38e01d7b480332258e9c375c7bbe94
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39553673"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스(MSSQLFDLauncher)에 대한 서비스 계정을 설정하거나 변경하는 방법에 대해 설명합니다. SQL Server 설치 프로그램에서 사용하는 기본 서비스 계정은 `NT Service\MSSQLFDLauncher`입니다.
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 정보
SQL Server 전체 텍스트 검색에서 전체 텍스트 검색 필터링 및 단어 분리를 처리하는 필터 데몬 호스트 프로세스를 시작하기 위해 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 사용됩니다. 전체 텍스트 검색을 사용하려면 이 시작 관리자 서비스를 실행해야 합니다.  
  
SQL 전체 텍스트 필터 데몬 시작 관리자 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스에 연결되는 인스턴스 인식형 서비스입니다. SQL 전체 텍스트 필터 데몬 시작 관리자 서비스는 서비스 계정 정보를 시작하는 각 필터 데몬 호스트 프로세스에 전파합니다.  

##  <a name="setting"></a> 서비스 계정 설정  
  
1.  **시작** 메뉴에서 **모든 프로그램**을 가리키고 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]를 확장한 다음 **SQL Server 2016 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 구성 관리자**에서 **SQL Server 서비스**를 클릭하고 **SQL 전체 텍스트 필터 데몬 시작 관리자(***인스턴스 이름***)** 를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 클릭합니다.  
  
3.  대화 상자의 **로그온** 탭을 클릭한 다음 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스에서 시작한 프로세스를 실행할 계정을 선택하거나 입력합니다.  
  
4.  대화 상자를 닫은 다음 **다시 시작** 을 클릭하여 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 다시 시작합니다.  
  
![SQL 전체 텍스트 필터 데몬 시작 프로세스 속성](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a> SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 시작되지 않은 경우 문제 해결  
 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 시작되지 않으면 다음과 같은 가능성 있는 원인을 검토합니다.  
  
### <a name="permissions-issues"></a>사용 권한 문제
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 있는 권한이 없습니다.  

     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정에 대한 사용 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에는 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 관리, 쿼리 및 시작하기 위한 기본 사용 권한이 부여됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 후 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹 사용 권한이 제거된 경우 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 없으며 전체 텍스트 검색이 비활성화됩니다.     

-   서비스에 로그인하는 데 사용된 계정에 권한이 없습니다.  
  
     서버 인스턴스가 설치된 컴퓨터에 대한 로그인 권한이 없는 계정을 사용 중일 수 있습니다. 로그인에 사용하는 계정에 로컬 컴퓨터에 대한 사용자 권한이 있는지 확인하십시오.  

### <a name="service-account-and-password-issues"></a>서비스 계정 및 암호 문제
-   서비스 계정의 사용자 계정 또는 암호가 잘못되었습니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 구성 관리자에서 서비스가 올바른 서비스 계정 및 암호를 사용하는지 확인합니다.  
  
-   SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정과 연결된 암호가 만료되었습니다.  
  
     SQL 전체 텍스트 필터 데몬 시작 관리자에 대해 로컬 사용자 계정을 사용하고 암호가 만료된 경우 다음을 수행해야 합니다.  
  
    1.  계정에 대한 새 Windows 암호를 설정합니다.  
  
    2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 구성 관리자에서 새 암호를 사용하도록 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 업데이트합니다.  
  
### <a name="named-pipes-configuration-issues"></a>명명된 파이프 구성 문제
-   SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 올바르게 구성되지 않았습니다.  
  
     로컬 컴퓨터에서 명명된 파이프 기능이 해제되었거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 기본 명명된 파이프 이외의 다른 명명된 파이프를 사용하도록 구성된 경우 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 없습니다.  
  
-   동일한 명명된 파이프의 다른 인스턴스가 이미 실행 중입니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 클라이언트에 대한 명명된 파이프 서버 역할을 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작되기 전에 다른 프로세스에서 이미 명명된 파이프를 만든 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 Windows 이벤트 로그에 오류가 기록되고 전체 텍스트 검색을 사용할 수 없게 됩니다.  동일한 명명된 파이프를 사용하고 응용 프로그램을 중지하려고 시도하는 프로세스 또는 응용 프로그램이 무엇인지 확인하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [서비스 관리 방법 도움말 항목&#40;SQL Server 구성 관리자&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
