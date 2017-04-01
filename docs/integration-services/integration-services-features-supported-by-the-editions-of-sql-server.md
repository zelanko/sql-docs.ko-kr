---
title: "SQL Server 버전에서 지원하는 Integration Services 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server 버전에서 지원하는 Integration Services 기능
 이 항목은 다른 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 SSIS(SQL Server Integration Services) 기능에 대한 세부 정보를 제공합니다.  

Evaluation 및 Developer 버전에서 지원하는 기능은 SQL Server Enterprise Edition을 참조하세요. 
  
최신 릴리스 정보 및 새로운 기능 정보는 다음을 참조하세요.
-   [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server vNext Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)
    
**SQL Server 2016 사용해보기**    

SQL Server Evaluation 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
    
> [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 가상 컴퓨터 소형](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)(SQL Server 2016이 이미 설치된 가상 컴퓨터 실행)**    

##  <a name="a-nameisanew-integration-services-features-in-sql-server-vnext"></a><a name="IS"></a>SQL Server vNext의 새로운 Integration Services 기능
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|규모 확장|예||||||예|
|OData 구성 요소에서 Microsoft Dynamics AX 및 Microsoft Dynamics CRM 지원 <sup>1</sup>|예|사용자 계정 컨트롤|||||예|

<sup>1</sup> 이 기능은 SQL Server 2016 서비스 팩 1에서도 지원됩니다.

##  <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|기본 제공 데이터 원본 커넥터|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|예|  
|Azure 데이터 원본 커넥터 및 태스크|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|예|  
|SQL Server 가져오기 및 내보내기 마법사|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|예|  
|Hadoop / HDFS 커넥터 및 태스크|예|사용자 계정 컨트롤|사용자 계정 컨트롤||||예|  
|SSIS 디자이너 및 런타임|예|사용자 계정 컨트롤|||||예|  
|기본 제공 태스크 및 변환|예|사용자 계정 컨트롤|||||예|  
|기본 데이터 프로파일링 도구|예|사용자 계정 컨트롤|||||예|  
|Attunity Oracle CDC Service|예||||||예|  
|Change Data Capture Designer for Oracle by Attunity|예||||||예| 

##  <a name="a-nameisaaa-integration-services---advanced-adapters"></a><a name="ISAA">Integration Services - 고급 어댑터</a>  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|성능 우선 Oracle 대상|예||||||예|  
|성능 우선 Teradata 대상|예||||||예|  
|SAP BW 원본 및 대상|예||||||예|  
|데이터 마이닝 모델 학습 대상 어댑터|예||||||예|  
|차원 처리 대상 어댑터|예||||||예|  
|파티션 처리 대상 어댑터|예||||||예|  
|Attunity의 변경 데이터 캡처 구성 요소|예||||||예|  
|Attunity의 Connector for ODBC(Open Database Connectivity)|예||||||예|  
  
##  <a name="a-nameisata-integration-services---advanced-transforms"></a><a name="ISAT"></a> Integration Services - 고급 변환  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|지속성(성능 우선) 조회|예||||||예|  
|데이터 마이닝 쿼리 변환|예||||||예|  
|유사 항목 그룹화 및 조회 변환|예||||||예|  
|용어 추출 및 조회 변환|예||||||예|  
  