---
title: SMO 설치 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8780920f4b535c77b82f404e84917d4cc97af4e1
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983885"
---
#<a name="installing-smo"></a>SMO 설치

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

이 페이지에서는 사용에 대 한 응용 프로그램 및 시스템 요구 사항을 SMO를 사용 하 여 SMO를 설치 하는 방법을 설명 합니다.

## <a name="smo-nuget-package"></a>SMO NuGet 패키지

부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO로 배포 되는 [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) SMO 사용 하 여 응용 프로그램을 개발할 수 있도록 NuGet 패키지.

이 SQL Server의 각 릴리스에 대 한 SQL 기능 팩의 일부로 이전에 릴리스된 SharedManagementObjects.msi 대체 합니다. SMO를 사용 하는 응용 프로그램 대신 NuGet 패키지를 사용 하도록 업데이트 해야 하 고 개발 중인 응용 프로그램을 사용 하 여 이진 파일은 설치 하도록 할 책임이 됩니다.

>>[!Important]
>>설명 했 듯이 합니다 [파일 및 버전 번호](files-and-version-numbers.md) 페이지에서 SMO 어셈블리를 GAC에 설치 하지 않아야 합니다. 이렇게도 SMO의 버전을 사용 하는 다른 응용 프로그램을 사용 하 여 문제가 발생할 수 있습니다 (같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

##<a name="installing-the-package"></a>패키지를 설치합니다.

참조 [NuGet 빠른 시작-패키지를 사용 하 여](https://docs.microsoft.com/nuget/quickstart/use-a-package) 지침과 예는 NuGet 패키지를 사용 하 여 설치 합니다. 
  
## <a name="system-requirements"></a>시스템 요구 사항
  
 SMO 필요 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0을 사용 하 여 응용 프로그램 클라이언트 컴퓨터는 버전이 또는 이상이 설치 되어 있는지 확인 해야 하므로 실행 합니다.
  
