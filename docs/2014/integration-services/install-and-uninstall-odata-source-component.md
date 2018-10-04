---
title: 설치 하 고 OData 원본 구성 요소를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 67bb3b093d63564c4eaae0144add029e569281f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068113"
---
# <a name="install-and-uninstall-odata-source-component"></a>OData 원본 구성 요소 설치 및 제거
  이 항목에서는 컴퓨터에서 OData 원본 구성 요소를 설치하거나 제거하기 위한 지침을 제공합니다.  
  
## <a name="installation"></a>설치  
 OData 원본 구성 요소를 사용하려면 다음과 같은 필수 구성 요소가 컴퓨터에 설치되어 있어야 합니다.  
  
-   SQL Server Data Tools(패키지를 디자인하는 데 사용)  
  
-   SQL Server Integration Services(Visual Studio 외부에서 패키지를 실행하는 데 사용)  
  
 OData 원본 구성 요소를 설치하려면 [SQL Server 2014 기능 팩](http://go.microsoft.com/fwlink/p/?LinkId=391999) 을 다운로드하고 다음 MSI 파일 중 하나를 실행합니다.  
  
-   ODataSourceForSQLServer2014-amd64.msi(64비트 플랫폼의 경우)  
  
-   ODataSourceForSQLServer2014-x86.msi(32비트 플랫폼의 경우)  
  
> [!IMPORTANT]  
>  64비트 설치 관리자는 32비트 및 64비트 버전의 OData 원본 구성 요소를 설치합니다. 32비트 OS를 사용하는 경우에는 32비트 설치 관리자를 실행해야 합니다.  
  
## <a name="uninstallation"></a>제거  
 OData 원본 구성 요소는 **프로그램 및 기능** 메뉴에서 제거할 수 있습니다. **Microsoft SQL Server SSIS OData 원본 구성 요소(x64)** 항목을 찾고 **제거**를 클릭합니다.  
  
  
