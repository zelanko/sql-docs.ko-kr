---
title: "SSRS의 Power BI 기술 미리 보기 보고서 - 릴리스 정보 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Reporting Services 릴리스 정보
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  2017년 1월 SQL Server Reporting Services의 Power BI 기술 미리 보기 보고서|

이 항목에서는 SQL Server Reporting Services의 Power BI 기술 미리 보기 보고서에서 나타나는 제한 사항 및 문제에 대해 설명합니다.

- 이 릴리스의 새로운 기능을 검토하려면 [Reporting Services의 새로운 기능](../reporting-services/ssrs-sql-server-reporting-services-의-새로운-기능.md)을 참조하세요.

 **사용해보기:**    
   -   [![Microsoft 다운로드 센터에서 다운로드](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351)  ** [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=839351)**에서 SQL Server Reporting Services 및 Power BI Desktop(SQL Server Reporting Services)의 Power BI 기술 미리 보기 보고서를 다운로드할 수 있습니다.


## <a name="january--2017"></a>2017년 1월

### <a name="report-server"></a>보고서 서버

- 이제 Https가 지원됩니다. 2016년 10월에 릴리스된 기술 미리 보기 VM에서는 사용할 수 없었습니다. 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.
   - PowerPoint 웹 뷰어 추가 기능을 사용하고 여기서 Power BI 보고서를 노출하려면 Https가 필요합니다.
- 이제 확장이 지원됩니다. 2016년 10월에 릴리스된 기술 미리 보기 VM에서는 사용할 수 없었습니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md)을 참조하세요.

### <a name="power-bi-reports"></a>Power BI 보고서

- Power BI 보고서를 SQL Server Reporting Services에서 사용하기 위해서는 Power BI Desktop(SQL Server Reporting Services)으로 생성해야 합니다. 평가 센터에서 Power BI Desktop(SQL Server Reporting Services)를 다운로드할 수 있습니다.
- Power BI 보고서는 Analysis Services(테이블 형식 또는 다차원 형식)에 대한 라이브 연결만 지원합니다.
- 사용자 지정 시각적 개체는 지원되지 않습니다.
- R 시각적 개체는 지원되지 않습니다.