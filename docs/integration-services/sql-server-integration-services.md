---
title: SQL Server Integration Services | Microsoft Docs
description: 엔터프라이즈 수준 데이터 통합 및 데이터 변환 솔루션을 빌드하기 위한 Microsoft 플랫폼인 SQL Server Integration Services에 대한 정보
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
keywords:
- SSIS
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6b4424cfb5311ee75bc6ea184b1fb25d0246b03b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724211"
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services

 > 이전 버전의 SQL Server와 관련된 내용은 [SQL Server Integration Services](sql-server-integration-services.md)를 참조하세요.

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 엔터프라이즈 수준 데이터 통합 및 데이터 변환 솔루션을 빌드하는 데 필요한 플랫폼입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 사용하여 파일을 복사 또는 다운로드하고, 데이터 웨어하우스를 로드하고, 데이터를 정리 및 마이닝하고, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체와 데이터를 관리하여 복잡한 비즈니스 문제를 해결합니다.

[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 XML 데이터 파일, 플랫 파일, 관계형 데이터 원본과 같은 다양한 원본에서 데이터를 추출 및 변환한 다음 하나 이상의 대상으로 로드할 수 있습니다.

[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 풍부한 기본 제공 작업 및 변환 집합, 패키지 빌드용 그래픽 도구 및 패키지를 저장, 실행 및 관리하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그 데이터베이스가 포함됩니다.

그래픽 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 도구를 사용하여 코드를 한 줄도 작성하지 않고 솔루션을 만들 수 있습니다. 광범위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델을 프로그래밍하여 패키지를 프로그래밍 방식으로 만들고 사용자 지정 태스크 및 기타 패키지 개체를 코딩할 수도 있습니다.

## <a name="get-sql-server-integration-services"></a>SQL Server Integration Services 가져오기

SQL Server에 SQL Server Integration Services를 설치하는 방법과 추가 다운로드에 대한 자세한 내용은 [Integration Services 설치](install-windows/install-integration-services.md)를 참조하세요.

##  <a name="infotipsql-servermediainfo-tippng-resources"></a>![info_tip](../sql-server/media/info-tip.png) 리소스
-   [SSIS 포럼에서 도움말 보기](https://social.msdn.microsoft.com/Forums/home?forum=sqlintegrationservices)
-   [Stack Overflow에서 도움말 보기](http://stackoverflow.com/questions/tagged/ssis)  
-   [SSIS 팀 블로그 수행](https://blogs.msdn.microsoft.com/ssis/)
-   [문제 보고 및 기능 요청](https://feedback.azure.com/forums/908035-sql-server)
-   [PC의 문서 가져오기](../sql-server/sql-server-help-installation.md)
