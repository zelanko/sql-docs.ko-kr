---
title: SQL Server 2014의 지원 되지 않는 MDS(Master Data Services) 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479439"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 MDS(Master Data Services) 기능
  이 항목에서는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]기능에 대해 설명합니다.  
  
## <a name="sssql14-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 지원되지 않는 기능  
 이 릴리스에서는 지원이 중단된 기능이 없습니다.  
  
## <a name="sssql11-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 지원되지 않는 기능  
  
### <a name="security"></a>보안  
 보안을 보다 쉽게 지정하기 위해 더 이상 파생 계층, 명시적 계층 및 특성 그룹 개체에 모델 개체 권한을 지정할 필요가 없습니다.  
  
-   파생 계층 권한은 이제 모델을 기반으로 합니다. 예를 들어 사용자에 게 파생 계층에 대 한 사용 권한을 부여 하려면 모델 개체에 **업데이트** 를 할당 해야 합니다. 그런 다음 사용자에 게 액세스 권한을 부여 하지 않으려는 엔터티에 대 한 **거부** 액세스를 할당할 수 있습니다.  
  
-   명시적 계층 권한은 이제 엔터티를 기반으로 합니다. 예를 들어 사용자가 계정 엔터티에 대 한 **업데이트** 권한을가지고 있으면 엔터티에 대 한 모든 명시적 계층을 업데이트할 수 있습니다.  
  
-   특성 그룹 권한은 더 이상 **사용자 및 그룹 권한** 기능 영역에서 할당할 수 없습니다. 대신 특성 그룹이 생성 되는 **시스템 관리** 기능 영역에서 사용자 및 그룹에 특성 그룹에 대 한 **업데이트** 권한을 부여할 수 있습니다. 특성 그룹에 대 한 **읽기 전용** 권한을 더 이상 사용할 수 없습니다.  
  
### <a name="staging-process"></a>준비 프로세스  
 새 준비 프로세스를 사용하여 다음을 수행할 수 없습니다.  
  
-   컬렉션 만들기 또는 삭제  
  
-   컬렉션에 멤버 추가 또는 컬렉션에서 멤버 제거  
  
-   멤버 또는 컬렉션 다시 활성화  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 준비 프로세스를 사용하여 컬렉션 작업을 할 수 있습니다.  
  
### <a name="model-deployment-wizard"></a>모델 배포 마법사  
 데이터를 포함하는 패키지는 더 이상 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 마법사를 사용하여 만들고 배포할 수 없습니다. 대신 새로운 명령줄 유틸리티를 사용할 수 있습니다. 자세한 내용은 [모델 배포&#40;Master Data Services&#41;](deploying-models-master-data-services.md)를 참조하세요.  
  
 데이터를 포함하지 않는 패키지는 계속해서 마법사를 사용하여 만들고 배포할 수 있습니다.  
  
 또한 패키지는 해당 패키지를 만드는 데 사용한 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에만 배포할 수 있습니다. 따라서 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 에서 만든 패키지는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에 배포할 수 없습니다. 먼저 패키지를 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 환경에 배포한 다음 데이터베이스를 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]로 업그레이드해야 합니다.  
  
### <a name="code-generation-business-rules"></a>코드 생성 비즈니스 규칙  
 코드 특성 값을 자동으로 생성하는 비즈니스 규칙이 이제 다르게 관리됩니다. 이전에는 코드 특성에 대 한 값을 생성 하기 위해 **비즈니스 규칙**의 **시스템 관리** 기능 영역에서 **생성 된 값 동작에 기본 특성** 을 사용 했습니다. 이제 **시스템 관리**에서 자동으로 생성 된 코드 값을 사용 하도록 엔터티를 편집 해야 합니다. 자세한 내용은 [MDS(Master Data Services)&#41;&#40;자동 코드 만들기 ](automatic-code-creation-master-data-services.md)를 참조 하세요.  
  
 이 유형의 규칙을 포함하는 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 모델 배포 패키지가 있는 경우 데이터베이스를 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]로 업그레이드할 때 비즈니스 규칙은 제외됩니다.  
  
### <a name="bulk-updates-and-exporting"></a>대량 업데이트 및 내보내기  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서는 더 이상 여러 멤버에 대한 특성 값을 대량으로 업데이트할 수 없습니다. 대량 업데이트를 수행 하려면 준비 프로세스 또는를 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]사용 합니다.  
  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서는 더 이상 멤버를 Excel로 내보낼 수 없습니다. Excel에서 멤버로 작업 하려면를 사용 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]합니다.  
  
### <a name="transactions"></a>의  
 사용자는 **탐색기** 기능 영역에서 더 이상 자신의 트랜잭션을 되돌릴 수 없습니다. 이전에는 사용자가 **탐색기**에서 데이터에 대 한 변경 내용을 되돌릴 수 있었습니다. 관리자는 **버전 관리** 기능 영역에서 모든 사용자에 대 한 트랜잭션을 되돌릴 수 있습니다.  
  
 주석은 이제 영구적이며 삭제할 수 없습니다. 이전에는 주석이 트랜잭션으로 간주되어 트랜잭션을 되돌리면 삭제할 수 있었습니다.  
  
### <a name="web-service"></a>웹 서비스  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 서비스는 이제 Silverlight의 요구에 따라 자동으로 설정됩니다. 이전에는 웹 서비스를 수동으로 설정해야 했습니다.  
  
### <a name="powershell-cmdlets"></a>PowerShell Cmdlet  
 MDS에는 PowerShell cmdlet이 더 이상 포함되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014에서 사용되지 않는 MDS(Master Data Services) 기능](deprecated-master-data-services-features.md)  
  
  
