---
title: "SQL Server의 R 런타임 관련 보안 고려 사항 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# SQL Server의 R 런타임 관련 보안 고려 사항
  이 항목에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 작업할 때의 보안 고려 사항에 대해 간략하게 설명합니다.  
  
 서비스를 관리하는 방법과 R 스크립트를 실행하는 데 사용되는 사용자 계정을 프로비전하는 방법에 대한 자세한 내용은 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)를 참조하세요.  
  
## 방화벽을 사용하여 R의 네트워크 액세스 제한  
 제안된 설치 방법에서는 Windows 방화벽 규칙을 사용하여 R 런타임 프로세스의 모든 아웃바운드 네트워크 액세스를 차단합니다. R 런타임 프로세스가 패키지를 다운로드하거나 악의적일 수 있는 기타 네트워크 호출을 수행하지 못하도록 하려면 방화벽 규칙을 만들어야 합니다.  
  
 Windows 방화벽 또는 원하는 기타 방화벽을 설정해 R 런타임의 네트워크 액세스를 차단하는 것이 좋습니다.  
  
 다른 방화벽 프로그램을 사용하는 경우에는 로컬 사용자 계정 또는 사용자 계정 풀이 나타내는 그룹에 대해 규칙을 설정하여 R 런타임에 대해 아웃바운드 네트워크 연결을 차단할 수도 있습니다.   
자세한 내용은 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)를 참조하세요.  
  
## 원격 계산 컨텍스트를 지 원하는 인증 방법 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 이제 간의 연결을 만들 때 모두 Windows 통합 인증 및 SQL 로그인을 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 원격 데이터 과학 클라이언트입니다. 
  
 예를 들어 랩톱에는 R 솔루션을 개발 하는 경우 SQL Server 컴퓨터에서 계산을 수행 하려면 만들게 됩니다 SQL Server 데이터 원본에서 R을 사용 하 여는 **rx** Windows 자격 증명을 기반으로 함수 및 연결 문자열을 정의 합니다. 변경 하는 경우는 _계산 컨텍스트_ 랩톱에 SQL Server 컴퓨터에서 Windows 계정에 필요한 권한이 있는 경우 모든 R 코드가 실행 됩니다 SQL Server 컴퓨터에 있습니다. 또한 사용자 자격 증명에서 R 코드의 일부로 실행 되는 모든 SQL 쿼리 실행 됩니다. 
 
 SQL 로그인을 SQL Server 데이터 원본에 대 한 연결 문자열에 사용할 수 있습니다, 있더라도 SQL Server 인스턴스 혼합된 모드 인증을 허용 하는 로그인 사용 해야 합니다.
 
 ### 암시 된 인증
  
 일반적으로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] R 런타임을 시작 하 고 자체 계정에서 R 스크립트를 실행 합니다. 그러나는 ODBC 호출을 수행 하는 R 스크립트의 경우는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 는 ODBC 호출 실패 하지 않으면 명령을 전송 하는 사용자의 자격 증명을 가장 합니다. 이 이라고 *묵시적된 인증*합니다. 
 
 > [!IMPORTANT] 
 >
 > 작업자 계정이 포함 된 Windows 사용자 그룹을 성공적으로 유추 된 인증에 대 한 (기본적으로 **SQLRUser**) 인스턴스와이 계정을 지정 해야 인스턴스에 연결 하는 권한을 대 한 master 데이터베이스에 계정이 있어야 합니다.  
  
## 미사용 데이터 암호화 지원되지 않음  
 R 런타임에서 보내거나 받는 데이터에 대해서는 투명한 데이터 암호화가 지원되지 않습니다. 따라서 R 스크립트에서 사용하는 데이터, 디스크에 저장된 데이터 또는 영구 저장된 중간 결과에는 미사용 데이터에 대한 암호화가 적용되지 **않습니다** .  
 
 ## 참고 항목
 [여기에 링크 설명을 입력 합니다.](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  