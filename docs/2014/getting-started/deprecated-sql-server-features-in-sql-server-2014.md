---
title: 사용 되지 않는 SQL Server 2014에서에서 SQL Server 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4abd066dd2fc971528468fb7104cb0c11e088150
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53348782"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 이후에는 사용되지 않는 SQL Server 기능
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 계속 제공되지만 더 이상 사용되지 않는 기능에 대해 설명합니다. 이러한 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 릴리스에서 제거될 예정입니다. 새 애플리케이션에는 이러한 기능을 사용하면 안 됩니다.  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않는 기능  
 아래의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않습니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하십시오. 기능 이름 열은 추적 이벤트에 ObjectName으로 표시되고 성능 카운터 및 sys.dm_os_performance_counters에 instance_name으로 표시됩니다. 기능 ID는 추적 이벤트에 ObjectId로 표시됩니다.  
  
|범주|사용되지 않는 기능|대체 기능|기능 이름|기능 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|데이터 프로그래밍 기능|[sys.soap_endpoints &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|WCF(Windows Communications Foundation) 또는 ASP.NET|네이티브 XML 웹 서비스|22|  
|데이터 프로그래밍 기능|[sys.endpoint_webmethods &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|WCF(Windows Communications Foundation) 또는 ASP.NET|네이티브 XML 웹 서비스|23|  
  
### <a name="slipstream-functionality"></a>통합 설치 기능  
 제품 업데이트 기능은 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1에서 제공했던 통합 설치 기능을 대체합니다. 따라서 통합 설치 기능과 관련된 명령줄 매개 변수, /*PCUSource* 및 /*CUSource*는 더 이상 사용되지 않습니다. 이러한 매개 변수는 계속 작동하지만 향후 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램 릴리스에서 제거될 수 있습니다. /*UpdateSource* 매개 변수는 통합 설치 매개 변수 /*PCUSource* 및 /*CUSource*의 기능을 결합합니다.  
  
 제공 했던 통합 설치 기능에 대 한 자세한 내용은 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1을 참조 하세요 [SQL Server 업데이트 통합 설치](https://go.microsoft.com/fwlink/?LinkId=219945) (https://go.microsoft.com/fwlink/?LinkId=219945)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)  
  
  
