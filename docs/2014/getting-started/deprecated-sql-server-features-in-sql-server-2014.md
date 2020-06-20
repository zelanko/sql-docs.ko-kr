---
title: SQL Server 2014에서 사용 되지 않는 SQL Server 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e4d888eee5ea6048d61007728bb436dabdccb8e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926997"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 이후에는 사용되지 않는 SQL Server 기능
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 계속 제공되지만 더 이상 사용되지 않는 기능에 대해 설명합니다. 이러한 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 릴리스에서 제거될 예정입니다. 새 애플리케이션에는 이러한 기능을 사용하면 안 됩니다.  
  
## <a name="features-not-supported-in-the-next-version-of-ssnoversion"></a>다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않는 기능  
 아래의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않습니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하십시오. 기능 이름 열은 추적 이벤트에 ObjectName으로 표시되고 성능 카운터 및 sys.dm_os_performance_counters에 instance_name으로 표시됩니다. 기능 ID는 추적 이벤트에 ObjectId로 표시됩니다.  
  
|Category|사용되지 않는 기능|대체 기능|기능 이름|기능 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|데이터 프로그래밍 기능|[soap_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|WCF(Windows Communications Foundation) 또는 ASP.NET|네이티브 XML 웹 서비스|22|  
|데이터 프로그래밍 기능|[endpoint_webmethods &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|WCF(Windows Communications Foundation) 또는 ASP.NET|네이티브 XML 웹 서비스|23|  
  
### <a name="slipstream-functionality"></a>통합 설치 기능  
 [제품 업데이트 기능은](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN) PCU1에서 제공 되는 통합 설치 기능에 대 한 확장으로 SQL Server 2012에서 도입 되었습니다 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] . SQL Server 2014에서 제품 업데이트 기능은 말합니다 SQL Server에 사용할 수 있는 권장 방법입니다. 따라서 원래 통합 설치 기능과 관련 된 명령줄 매개 변수,/*Pcusource* 및/*CUSource*는 더 이상 사용할 수 없습니다. 이러한 매개 변수는 계속 작동 하지만 향후 설치 프로그램 릴리스에서 제거 될 수 있습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . 사용 하기에 권장 되는 매개 변수는/*UpdateSource* 입니다 .이 매개 변수는 원래 통합 설치 매개 변수,/*pcusource* 및/*CUSource*의 기능을 결합 합니다.  
  
 PCU1에서 제공 되는 통합 설치 기능에 대 한 자세한 내용은 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [통합 설치 a SQL Server Update](https://go.microsoft.com/fwlink/?LinkId=219945) (를 참조 하세요 https://go.microsoft.com/fwlink/?LinkId=219945) .  
 /*UpdateSource* 를 사용 하 여 SQL Server 빌드를 통합 설치 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.
 
 - [업데이트 된 설치 패키지를 사용 하 SQL Server 2012 설치 프로그램을 패치 하는 방법 (UpdateSource을 사용 하 여 스마트 설치를 가져오는 방법)](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server 2012 설치가 더 효율적입니다.](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>참고 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)  
  
  
