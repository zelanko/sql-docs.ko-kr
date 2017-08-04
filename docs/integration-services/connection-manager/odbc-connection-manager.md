---
title: "ODBC 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a136e71727d1a0b729f7014448dd97d81a7af89d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-connection-manager"></a>ODBC 연결 관리자
  ODBC 연결 관리자를 사용하면 패키지에서 ODBC(Open Database Connectivity) 사양을 사용하여 다양한 데이터베이스 관리 시스템에 연결할 수 있습니다.  
  
 패키지에 ODBC 연결을 추가하고 연결 관리자 속성을 설정할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 연결 관리자를 만들고 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 런타임 시 연결 관리자는 물리적 ODBC 연결로 확인됩니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **ODBC**로 설정됩니다.  
  
 다음과 같은 방법으로 ODBC 연결 관리자를 구성할 수 있습니다.  
  
-   사용자 또는 시스템 데이터 원본 이름을 참조하는 연결 문자열을 제공합니다.  
  
-   연결할 서버를 지정합니다.  
  
-   런타임 시 연결이 유지되는지 여부를 나타냅니다.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>ODBC 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [ODBC 연결 관리자 UI 참조](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
