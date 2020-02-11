---
title: SQL Server Compact Edition 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 752c825cb34fbf2afe5d2306afbd562a49f74b7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833148"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 연결 관리자
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 사용하면 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결할 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 포함 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] compact 대상은이 연결 관리자를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compact 데이터베이스의 테이블에 데이터를 로드 합니다.  
  
> [!NOTE]  
>  64비트 컴퓨터에서는 32비트 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터 원본에 연결하는 패키지를 실행해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 데이터 원본에 연결할 때 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 공급자는 32비트 버전에서만 사용할 수 있습니다.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 연결 관리자 구성  
 패키지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compact 연결 관리자를 추가 하면에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compact 연결로 확인 되는 연결 관리자를 만들고, 연결 관리자 속성을 설정 하 고, 연결 관리자를 패키지의 `Connections` 컬렉션에 추가 합니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `SQLMOBILE`로 설정됩니다.  
  
 다음과 같은 방법으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 구성할 수 있습니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스의 위치를 지정하는 연결 문자열을 제공합니다.  
  
-   암호로 보호되는 데이터베이스에 대한 암호를 제공합니다.  
  
-   데이터베이스가 저장된 서버를 지정합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SQL Server Compact Edition 연결 관리자 편집기 &#40;연결 페이지&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [모든 페이지&#41;&#40;SQL Server Compact Edition 연결 관리자 편집기](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
  
