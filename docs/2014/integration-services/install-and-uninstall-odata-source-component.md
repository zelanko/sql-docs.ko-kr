---
title: OData 원본 구성 요소 설치 및 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eeeea240761915fae8489072cc71d697b988ce7e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965463"
---
# <a name="install-and-uninstall-odata-source-component"></a>OData 원본 구성 요소 설치 및 제거
  이 항목에서는 컴퓨터에서 OData 원본 구성 요소를 설치하거나 제거하기 위한 지침을 제공합니다.  
  
## <a name="installation"></a>설치  
 OData 원본 구성 요소를 사용하려면 다음과 같은 필수 구성 요소가 컴퓨터에 설치되어 있어야 합니다.  
  
-   SQL Server Data Tools(패키지를 디자인하는 데 사용)  
  
-   SQL Server Integration Services(Visual Studio 외부에서 패키지를 실행하는 데 사용)  
  
 OData 원본 구성 요소를 설치하려면 [SQL Server 2014 기능 팩](https://go.microsoft.com/fwlink/p/?LinkId=391999) 을 다운로드하고 다음 MSI 파일 중 하나를 실행합니다.  
  
-   ODataSourceForSQLServer2014-amd64.msi(64비트 플랫폼의 경우)  
  
-   ODataSourceForSQLServer2014-x86.msi(32비트 플랫폼의 경우)  
  
> [!IMPORTANT]  
>  64비트 설치 관리자는 32비트 및 64비트 버전의 OData 원본 구성 요소를 설치합니다. 32비트 OS를 사용하는 경우에는 32비트 설치 관리자를 실행해야 합니다.  
  
## <a name="uninstallation"></a>제거  
 OData 원본 구성 요소는 **프로그램 및 기능** 메뉴에서 제거할 수 있습니다. **Microsoft SQL Server SSIS OData 원본 구성 요소(x64)** 항목을 찾고 **제거**를 클릭합니다.  
  
  
