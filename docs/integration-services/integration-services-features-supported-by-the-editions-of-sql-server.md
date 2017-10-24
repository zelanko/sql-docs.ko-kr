---
title: "Integration Services의 SQL Server 버전에서 지 원하는 기능 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: e9d1b8851f113fa44264230a79d0e496007ed96b
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>SQL Server 버전에서 지 원하는 integration Services 기능
 이 항목은 다른 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]버전에서 지원되는 SSIS(SQL Server Integration Services) 기능에 대한 세부 정보를 제공합니다.  

Evaluation 및 Developer 버전에서 지 원하는 기능, Enterprise Edition에 대 한 다음 표에 나열 된 기능을 참조 하세요.
  
최신 릴리스 정보 및 새로운 정보에 대 한 다음 문서를 참조 합니다.
-   [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server 2017 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016을 사용해 보세요.**    

SQL Server Evaluation 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
    
> [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>SQL Server 2017의 새로운 Integration Services 기능
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|마스터 확장|예|||||
|작업자 확장|예|예 <sup>1</sup>|TBD|TBD|TBD|
|OData 구성 요소에서 Microsoft Dynamics AX 및 Microsoft Dynamics CRM에 대 한 지원 <sup>2</sup>|예|예||||

<sup>1</sup> 스케일 아웃 작업자 SQL Server Enterprise의 인스턴스에서 실행 해야 범위 확장의 엔터프라이즈 전용 기능을 필요로 하는 패키지를 실행 합니다.

<sup>2</sup> 이 기능은 SQL Server 2016 서비스 팩 1 에서도 지원 됩니다.

## <a name="IEWiz"></a>SQL Server 가져오기 및 내보내기 마법사

|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server 가져오기 및 내보내기 마법사|예|예|예|예|예|  

## <a name="IS"></a> Integration Services  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|기본 제공 데이터 원본 커넥터|예|예|||| 
|기본 제공 태스크 및 변환|예|예||||  
|ODBC 원본 및 대상 by Attunity|예|예|||| 
|Azure 데이터 원본 커넥터 및 태스크|예|예||||  
|Hadoop/HDFS 커넥터 및 태스크|예|예||||  
|기본 데이터 프로파일링 도구|예|예|||| 

## <a name="ISAA"></a>Integration Services-고급 원본 및 대상  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|성능 우선 Oracle 원본 및 대상 by Attunity|예|||||  
|성능 우선 Teradata 원본 및 대상 by Attunity|예|||||  
|SAP BW 원본 및 대상|예|||||  
|데이터 마이닝 모델 학습 대상|예|||||  
|차원 처리 대상|예|||||  
|파티션 처리 대상|예|||||  
  
## <a name="ISAT"></a>Integration Services-고급 태스크 및 변환  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|변경 데이터 캡처 구성 요소 attunity <sup>1</sup>|예|||||  
|데이터 마이닝 쿼리 변환|예|||||  
|유사 항목 그룹화 및 유사 항목 조회 변환|예|||||  
|용어 추출 및 용어 조회 변환|예|||||  

<sup>1</sup> by Attunity의 변경 데이터 캡처 구성 요소에는 Enterprise edition 필요 합니다. 그러나 Change Data Capture Service 및 Change Data Capture Designer 필요 하지 않습니다 Enterprise edition. 사용할 수 있습니다는 디자이너와 서비스는 컴퓨터에서 SSIS 설치 되어 있지 않습니다.
