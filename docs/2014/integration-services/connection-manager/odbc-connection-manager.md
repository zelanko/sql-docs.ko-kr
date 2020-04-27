---
title: ODBC 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6c7ecd59bcf3a3ece0d61ecbb428bb39a80068f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833765"
---
# <a name="odbc-connection-manager"></a>ODBC 연결 관리자
  ODBC 연결 관리자를 사용하면 패키지에서 ODBC(Open Database Connectivity) 사양을 사용하여 다양한 데이터베이스 관리 시스템에 연결할 수 있습니다.  
  
 패키지에 ODBC 연결을 추가 하 고 연결 관리자 속성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 을 설정할 때는 연결 관리자를 만들고 패키지의 `Connections` 컬렉션에 연결 관리자를 추가 합니다. 런타임 시 연결 관리자는 물리적 ODBC 연결로 확인됩니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `ODBC`로 설정됩니다.  
  
 다음과 같은 방법으로 ODBC 연결 관리자를 구성할 수 있습니다.  
  
-   사용자 또는 시스템 데이터 원본 이름을 참조하는 연결 문자열을 제공합니다.  
  
-   연결할 서버를 지정합니다.  
  
-   런타임 시 연결이 유지되는지 여부를 나타냅니다.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>ODBC 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [ODBC 연결 관리자 UI 참조](../odbc-connection-manager-ui-reference.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
