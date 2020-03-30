---
title: SQL Server Compact Edition 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.connection.f1
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62c5a0400918ffe86cca4ec9ff98dd9254d29621
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294348"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 사용하면 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 대상은 이 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 테이블에 데이터를 로드합니다.  
  
> [!NOTE]  
>  64비트 컴퓨터에서는 32비트 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터 원본에 연결하는 패키지를 실행해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 데이터 원본에 연결할 때 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 공급자는 32비트 버전에서만 사용할 수 있습니다.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 연결 관리자 구성  
 패키지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결로 확인되는 연결 관리자를 만들고 연결 관리자 속성을 설정하며 패키지의 **Connections** 컬렉션에 연결 관리자를 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **SQLMOBILE**로 설정됩니다.  
  
 다음과 같은 방법으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 구성할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 위치를 지정하는 연결 문자열을 제공합니다.  
  
-   암호로 보호되는 데이터베이스에 대한 암호를 제공합니다.  
  
-   데이터베이스가 저장된 서버를 지정합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="sql-server-compact-edition-connection-manager-editor-connection-page"></a>SQL Server Compact Edition 연결 관리자 편집기(연결 페이지)
  **SQL Server Compact Edition 연결 관리자** 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결하기 위한 속성을 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 연결 관리자에 대한 자세한 내용은 [SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)를 참조하세요.  
  
### <a name="options"></a>옵션  
 **데이터베이스 파일 이름 및 경로 입력**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 경로 및 파일 이름을 입력합니다.  
  
 **찾아보기**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server Compact Edition 데이터베이스 선택 **대화 상자를 사용하여 원하는** Compact 데이터베이스 파일을 찾습니다.  
  
 **데이터베이스 암호 입력**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 암호를 입력합니다.  
  
## <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>SQL Server Compact Edition 연결 관리자 편집기(모든 페이지)
  **SQL Server Compact Edition 연결 관리자** 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결하기 위한 속성을 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 연결 관리자에 대한 자세한 내용은 [SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)를 참조하세요.  
  
### <a name="options"></a>옵션  
 **자동 축소 임계값**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에서 자동 축소 프로세스를 실행하기 전에 허용되는 사용 가능한 공간(%)을 지정합니다.  
  
 **기본 잠금 에스컬레이션**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스가 잠금 에스컬레이션 전에 획득하는 데이터베이스 잠금 수를 지정합니다.  
  
 **기본 잠금 제한 시간**  
 트랜잭션에서 잠금을 대기할 기본 간격(밀리초)을 지정합니다.  
  
 **플러시 간격**  
 커밋된 트랜잭션을 디스크에 플러시하는 간격(초)을 지정합니다.  
  
 **로캘 ID**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 LCID(로캘 ID)를 지정합니다.  
  
 **최대 버퍼 크기**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact에서 데이터를 디스크에 플러시하기 전에 사용하는 최대 메모리 용량(KB)을 지정합니다.  
  
 **최대 데이터베이스 크기**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 최대 크기(MB)를 지정합니다.  
  
 **모드**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스를 열 파일 모드를 지정합니다. 이 속성의 기본값은 **읽기/쓰기**입니다.  
  
 다음 표에서는 모드 옵션의 4가지 값에 대해 설명합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**읽기 전용**|데이터베이스에 대한 읽기 전용 액세스 권한을 지정합니다.|  
|**읽기/쓰기**|데이터베이스에 대한 읽기/쓰기 권한을 지정합니다.|  
|**단독**|데이터베이스에 대한 단독 액세스 권한을 지정합니다.|  
|**공유 읽기**|다른 사용자가 데이터베이스를 동시에 읽을 수 있도록 지정합니다.|  
  
 **Persist Security Info**  
 보안 정보를 연결 문자열의 일부로 반환할지 여부를 지정합니다. 이 옵션의 기본값은 **False**입니다.  
  
 **임시 파일 디렉터리**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 임시 데이터베이스 파일의 위치를 지정합니다.  
  
 **데이터 원본**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 이름을 지정합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 암호를 입력합니다.  
  
