---
title: SMO의 이전 버전과 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f4fcb8eedf3bfc326675bd26a03083de86afaa68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="backward-compatibility-in-smo"></a>SMO의 이전 버전과의 호환성
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 작성된 SMO 응용 프로그램은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 SMO를 사용하여 다시 컴파일할 수 있습니다.  
  
## <a name="migrating-smo-applications"></a>SMO 응용 프로그램 마이그레이션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 SMO dll 참조를 제거하고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 제공되는 새 SMO dll에 대한 참조를 포함해야 합니다.  
  
 다음은 반드시 참조해야 할 항목입니다.  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 이러한 파일은 연결 클래스, SMO 유틸리티 클래스 및 기본 클래스입니다.  
  
> [!NOTE]  
>  SmoEnum.dll은 제거되었으므로 이에 대한 참조는 SMO [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 프로젝트에서 제거해야 합니다.  
  
 네임스페이스도 변경되어 다음과 같이 사용할 수 있습니다.  
  
##### <a name="for-visual-c"></a>Visual C#의 경우  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>Visual Basic의 경우  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 코드에서 **Server.GetSqlSmoObject(Urn)**와 같은 URN 기능을 사용하는 경우 Microsoft.SqlServer.Management.Sdk.Sfc 네임스페이스에 연결해야 합니다.  
  
 코드에서 직접 전송 개체를 사용하는 경우 Microsoft.SqlServer.Management.SmoExtended 네임스페이스에 연결해야 합니다.  
  
 코드를 마이그레이션할 때 코드를 수정해야 할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 몇 가지 기능이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 더 이상 사용되지 않기 때문입니다. 사용 되지 않는 기능에 대 한 자세한 내용은 참조 [Database Engine Features in SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) 에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 온라인 설명서.  
  
  
