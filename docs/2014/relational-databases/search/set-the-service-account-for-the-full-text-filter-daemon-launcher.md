---
title: 전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정 | Microsoft 문서
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d702e1dcf8bc710324e7593ebe469317d9f43e68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63237900"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스(MSSQLFDLauncher)에 대한 서비스 계정을 설정하는 방법에 대해 설명합니다. 전체 텍스트 검색 ssNoVersionto에서 전체 텍스트 검색 필터링 및 단어 분리를 처리하는 필터 데몬 호스트 프로세스를 시작하기 위해 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 사용됩니다. 전체 텍스트 검색을 사용하려면 이 서비스를 실행해야 합니다.  
  
 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스에 연결되는 인스턴스 인식형 서비스입니다. SQL 전체 텍스트 필터 데몬 시작 관리자 서비스는 서비스 계정 정보를 각 필터 데몬 호스트 프로세스에 전파합니다.  
  
  
##  <a name="setting"></a> 서비스 계정 설정  
  
#### <a name="to-set-the-sql-full-text-filter-daemon-launcher-service-account-for-full-text-search"></a>전체 텍스트 검색용 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정을 설정하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 구성 관리자**, 클릭 **SQL Server Services**를 마우스 오른쪽 단추로 클릭 **SQL 전체 텍스트 필터 데몬 시작 관리자 (*`instance name`*)** 를 클릭 하 고 **속성**합니다.  
  
3.  대화 상자의 **로그온** 탭을 클릭한 다음 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스에서 만든 각 프로세스를 실행할 계정을 선택하거나 입력합니다.  
  
4.  대화 상자를 닫은 다음 **다시 시작** 을 클릭하여 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 다시 시작합니다.  
  
  
##  <a name="error"></a> SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 시작 되지 않습니다.  
 다음과 같은 경우 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 시작되지 않을 수 있습니다.  
  
-   SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정과 연결된 암호가 만료되었습니다.  
  
     SQL 전체 텍스트 필터 데몬 시작 관리자에 대해 로컬 사용자 계정을 사용하고 암호가 만료될 경우 다음을 수행해야 합니다.  
  
    1.  계정에 대한 새 Windows 암호를 설정합니다.  
  
    2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 새 암호를 사용하도록 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 업데이트합니다.  
  
-   서비스 계정의 사용자 계정 또는 암호가 잘못되었습니다.  
  
     SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 잘못된 사용자 계정 및 암호로 로그인을 시도할 수 있습니다. 위 절차에 따라 서비스에 대한 사용자 계정이 변경되지 않았는지 확인하십시오.  
  
-   서비스에 로그인하는 데 사용된 계정에 권한이 없습니다.  
  
     서버 인스턴스가 설치된 컴퓨터에 대한 로그인 권한이 없는 계정을 사용 중일 수 있습니다. 로그인에 사용하는 계정에 로컬 컴퓨터에 대한 사용자 권한이 있는지 확인하십시오.  
  
-   동일한 명명된 파이프의 다른 인스턴스가 이미 실행 중입니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 클라이언트에 대한 명명된 파이프 서버 역할을 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작되기 전에 다른 프로세스에서 이미 명명된 파이프를 만든 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 Windows 이벤트 로그에 오류가 기록되고 전체 텍스트 검색을 사용할 수 없게 됩니다.  동일한 명명된 파이프를 사용하고 애플리케이션을 중지하려고 시도하는 프로세스 또는 애플리케이션이 무엇인지 확인하십시오.  
  
-   SQL 전체 텍스트 필터 데몬 시작 관리자 서비스가 올바르게 구성되지 않았습니다.  
  
     로컬 컴퓨터에서 서비스가 올바르게 구성되어 있지 않을 수 있습니다.  
  
     로컬 컴퓨터에서 명명된 파이프 기능이 해제되었거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 기본 명명된 파이프 이외의 다른 명명된 파이프를 사용하도록 구성된 경우 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 있는 권한이 없습니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에는 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 관리, 쿼리 및 시작하기 위한 기본 사용 권한이 부여됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 후 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹 사용 권한이 제거된 경우 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스를 시작할 수 없으며 전체 텍스트 검색이 비활성화됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에 SQL 전체 텍스트 필터 데몬 시작 관리자 서비스 계정에 대한 사용 권한이 있는지 확인하세요.  
  
  
## <a name="see-also"></a>관련 항목  
 [서비스 관리 방법 도움말 항목&#40;SQL Server 구성 관리자&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)  
  
  
