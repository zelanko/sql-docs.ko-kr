---
description: SMO 설치
title: SMO 설치 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15ce6ea1c72bee64ad8fe96e70b9a7c513c623e6
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868271"
---
# <a name="installing-smo"></a>SMO 설치

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

이 페이지에서는 응용 프로그램에서 사용할 SMO를 설치 하 고 SMO를 사용 하기 위한 시스템 요구 사항에 대 한 정보를 제공 합니다.

## <a name="smo-nuget-package"></a>SMO NuGet 패키지

2017 SMO부터 smo를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 응용 프로그램을 개발할 수 있도록 [Microsoft sql server](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 패키지로 배포 됩니다.

이는 SQL Server의 각 릴리스에 대 한 SQL 기능 팩의 일부로 이전에 출시 된 SharedManagementObjects.msi를 대체 한 것입니다. SMO를 사용 하는 응용 프로그램은 NuGet 패키지를 대신 사용 하도록 업데이트 되어야 하며, 개발 중인 응용 프로그램과 함께 이진 파일이 설치 되도록 해야 합니다.

>>[!Important]
>>[파일 및 버전 번호](files-and-version-numbers.md) 페이지에 설명 된 대로 SMO 어셈블리를 GAC에 설치 하면 안 됩니다. 이렇게 하면 해당 버전의 SMO (예: Management Studio)도 사용 하는 다른 응용 프로그램에서 문제가 발생할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="installing-the-package"></a>패키지 설치

Nuget 패키지 설치 및 사용에 대 한 지침과 예제는 [nuget 빠른 시작-패키지 사용](/nuget/quickstart/use-a-package) 을 참조 하세요. 
  
## <a name="system-requirements"></a>시스템 요구 사항
  
 SMO를 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 실행 하려면 4.0 또는 .Net Core 2.0이 필요 하므로이를 사용 하는 응용 프로그램은 클라이언트 컴퓨터에 해당 버전 이상이 설치 되어 있는지 확인 해야 합니다. NetFx SMO 라이브러리와 함께 설치 되는 일부 네이티브 이진 파일에는 VC 2013 runtime도 설치 해야 합니다. 해당 런타임은 패키지에 포함 되지 않습니다. 다음에서 대상 아키텍처에 적절 한 재배포 가능 패키지를 다운로드할 수 있습니다. https://www.microsoft.com/download/details.aspx?id=40784
