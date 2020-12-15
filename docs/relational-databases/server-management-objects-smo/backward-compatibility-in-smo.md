---
description: SMO의 이전 버전과의 호환성
title: SMO의 이전 버전과의 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6e36a0966f631138768c2c4b17ab7444df76aea
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463074"
---
# <a name="backward-compatibility-in-smo"></a>SMO의 이전 버전과의 호환성
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 작성된 SMO 애플리케이션은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 SMO를 사용하여 다시 컴파일할 수 있습니다.  
  
## <a name="migrating-smo-applications"></a>SMO 애플리케이션 마이그레이션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 SMO dll 참조를 제거하고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 제공되는 새 SMO dll에 대한 참조를 포함해야 합니다.  
  
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
  
 코드에서 **Server.GetSqlSmoObject(Urn)** 와 같은 URN 기능을 사용하는 경우 Microsoft.SqlServer.Management.Sdk.Sfc 네임스페이스에 연결해야 합니다.  
  
 코드에서 직접 전송 개체를 사용하는 경우 Microsoft.SqlServer.Management.SmoExtended 네임스페이스에 연결해야 합니다.  
  
 코드를 마이그레이션할 때 코드를 수정해야 할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 의 몇 가지 기능이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 더 이상 사용되지 않기 때문입니다. 사용 되지 않는 기능에 대 한 자세한 내용은 온라인 설명서의 [SQL Server 2016에서 사용 되지 않는 데이터베이스 엔진 기능](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) 을 참조 하십시오 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
  
