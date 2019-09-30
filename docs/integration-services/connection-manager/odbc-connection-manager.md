---
title: ODBC 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.odbcconnection.f1
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0d115753447a337cc9846942e2c39da54f3658f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298493"
---
# <a name="odbc-connection-manager"></a>ODBC 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="odbc-connection-manager-ui-reference"></a>ODBC 연결 관리자 UI 참조
  **ODBC 연결 관리자 구성** 대화 상자를 사용하여 ODBC 데이터 원본에 대한 연결을 추가할 수 있습니다.  
  
 ODBC 연결 관리자에 대한 자세한 내용은 [ODBC Connection Manager](../../integration-services/connection-manager/odbc-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **데이터 연결**  
 목록에서 기존 ODBC 연결 관리자를 선택합니다.  
  
 **데이터 연결 속성**  
 선택한 ODBC 연결 관리자의 속성과 값을 표시합니다.  
  
 **새로 만들기**  
 **연결 관리자** 대화 상자를 사용하여 ODBC 연결 관리자를 만듭니다. 필요하면 이 대화 상자에서 새 ODBC 데이터 원본을 만들 수도 있습니다.  
  
 **Delete**  
 연결을 선택한 다음 **삭제** 단추를 사용하여 삭제합니다.  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
