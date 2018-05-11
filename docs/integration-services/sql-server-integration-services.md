---
title: SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
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
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0cbe57fde9348e096ff365189ae82558601b724f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services

 > 이전 버전의 SQL Server와 관련된 내용은 [SQL Server Integration Services](https://msdn.microsoft.com/library/ms141026(SQL.120).aspx)를 참조하세요.

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 엔터프라이즈 수준 데이터 통합 및 데이터 변환 솔루션을 빌드하는 데 필요한 플랫폼입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 파일을 복사 또는 다운로드하고 이벤트에 응답하여 전자 메일 메시지를 보내며 데이터 웨어하우스를 업데이트하고 데이터를 정리 및 마이닝하며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체와 데이터를 관리하여 복잡한 비즈니스 문제를 해결할 수 있습니다. 패키지는 단독으로 또는 다른 패키지와 함께 작동하여 복잡한 비즈니스 요구를 처리할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 XML 데이터 파일, 플랫 파일, 관계형 데이터 원본과 같은 다양한 원본에서 데이터를 추출 및 변환한 다음 하나 이상의 대상으로 로드할 수 있습니다.<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 다양한 기본 제공 태스크와 변환 집합, 패키지 생성 도구, 패키지 실행 및 관리를 위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 포함되어 있습니다. 그래픽 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 도구를 사용하여 코드를 한 줄도 작성하지 않고 솔루션을 만들거나 광범위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델을 프로그래밍하여 패키지를 프로그래밍 방식으로 만들고 사용자 지정 태스크 및 기타 패키지 개체를 코딩할 수 있습니다.

## <a name="try-sql-server-and-sql-server-integration-services"></a>SQL Server 및 SQL Server Integration Services 평가판 다운로드
- [![평가 센터에서 다운로드](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [SQL Server 2017 또는 2016 다운로드](https://www.microsoft.com/evalcenter/evaluate-sql-server)
- [![평가 센터에서 다운로드](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)
- [![평가 센터에서 다운로드](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)

##  <a name="infotipsql-servermediainfo-tippng-resources"></a>![info_tip](../sql-server/media/info-tip.png) 리소스
-   [SSIS 포럼에서 도움말 보기](https://social.msdn.microsoft.com/Forums/home?forum=sqlintegrationservices)
-   [Stack Overflow에서 도움말 보기](http://stackoverflow.com/questions/tagged/ssis)  
-   [SSIS 팀 블로그 수행](https://blogs.msdn.microsoft.com/ssis/)
-   [문제 보고 및 기능 요청](https://feedback.azure.com/forums/908035-sql-server)
-   [PC의 문서 가져오기](../sql-server/sql-server-help-installation.md)
