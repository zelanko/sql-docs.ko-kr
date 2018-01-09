---
title: "SMO 설치 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5d758997c68328cd984befcf808721336c18ece4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
#<a name="installing-smo"></a>SMO 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 페이지에서는 SMO를 사용 하는 시스템 요구 사항, 응용 프로그램에서 사용 하기 위해 SMO를 설치 하는 방법을 설명 합니다.

## <a name="smo-nuget-package"></a>SMO NuGet 패키지

부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO로 배포는 [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 패키지를 사용자가 SMO와 응용 프로그램을 개발할 수 있도록 합니다.

SQL Server의 각 릴리스에 대 한 SQL 기능 팩의 일부로 이전에 릴리스된 SharedManagementObjects.msi에 대 한 대체입니다. SMO를 사용 하는 응용 프로그램 대신 NuGet 패키지를 사용 하도록 업데이트 해야 하 고 개발 중인 응용 프로그램으로는 바이너리가 설치 된 것을 확인 합니다 됩니다.

>>[!Important]
>>설명 했 듯이 [파일 및 버전 번호](files-and-version-numbers.md) 페이지에서 SMO 어셈블리를 GAC에 설치 하지 않아야 합니다. 이렇게 해당 버전의 SMO 사용 하는 다른 응용 프로그램에 문제가 발생할 수 없습니다 (예: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

##<a name="installing-the-package"></a>패키지 설치

참조 [NuGet 빠른 시작-패키지를 사용 하 여](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package) 지침과 예는 NuGet 패키지를 사용 하 여 설치 합니다. 
  
## <a name="system-requirements"></a>시스템 요구 사항
  
 SMO 필요 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0을 사용 하는 모든 응용 프로그램 클라이언트 컴퓨터가 해당 버전 또는 이상이 설치를 확인 해야 하므로 실행 합니다.
  
