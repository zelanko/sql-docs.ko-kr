---
title: SQL Server 버전에서 지원하는 Integration Services 기능 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ac646cd235a6307fdcebcd48d42a368f4973df89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057616"
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>SQL Server 버전에서 지원하는 Integration Services 기능

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 이 항목은 다른 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]버전에서 지원되는 SSIS(SQL Server Integration Services) 기능에 대한 세부 정보를 제공합니다.  

평가 버전 및 디벨로퍼 버전에서 지원되는 기능은 다음 테이블의 엔터프라이즈 버전에 나열된 기능을 참조하세요.
  
최신 릴리스 정보 및 새로운 기능 정보는 다음 문서를 참조하세요.
-   [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server 2017 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016을 사용해 보세요.**    

SQL Server Evaluation 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
    
> [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>SQL Server 2017의 새로운 Integration Services 기능
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Scale Out 마스터|예|||||
|Scale Out 작업자|예|예 <sup>1</sup>|TBD|TBD|TBD|
|OData 구성 요소에서 Microsoft Dynamics AX 및 Microsoft Dynamics CRM 지원 <sup>2</sup>|예|예||||

<sup>1</sup> Scale Out에서 엔터프라이즈 전용 기능이 필요한 패키지를 실행하는 경우 SQL Server Enterprise 인스턴스에서도 Scale Out 작업자를 실행해야 합니다.

<sup>2</sup> 이 기능은 SQL Server 2016 서비스 팩 1에서도 지원됩니다.

## <a name="IEWiz"></a> SQL Server 가져오기 및 내보내기 마법사

|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server 가져오기 및 내보내기 마법사|예|예|예|예|예|  

## <a name="IS"></a> Integration Services  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|기본 제공 데이터 원본 커넥터|예|예|||| 
|기본 제공 태스크 및 변환|예|예||||  
|ODBC 원본 및 대상 |예|예|||| 
|Azure 데이터 원본 커넥터 및 태스크|예|예||||  
|Hadoop/HDFS 커넥터 및 태스크|예|예||||  
|기본 데이터 프로파일링 도구|예|예|||| 

## <a name="ISAA"></a> Integration Services - 고급 원본 및 대상  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Attunity에 의한 고성능 Oracle 원본 및 대상|예|||||  
|Attunity에 의한 고성능 Teradata 원본 및 대상|예|||||  
|SAP BW 원본 및 대상|예|||||  
|데이터 마이닝 모델 학습 대상|예|||||  
|차원 처리 대상|예|||||  
|파티션 처리 대상|예|||||  
  
## <a name="ISAT"></a> Integration Services - 고급 작업 및 변환  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Attunity의 변경 데이터 캡처 구성 요소 <sup>1</sup>|예|||||  
|데이터 마이닝 쿼리 변환|예|||||  
|유사 항목 그룹화 및 유사 항목 조회 변환|예|||||  
|용어 추출 및 용어 조회 변환|예|||||  

<sup>1</sup> Attunity의 변경 데이터 캡처 구성 요소에는 엔터프라이즈 버전이 필요합니다. 단, 변경 데이터 캡처 서비스 및 변경 데이터 캡처 디자이너에는 엔터프라이즈 버전이 필요하지 않습니다. SSIS가 설치되지 않은 컴퓨터에서 디자이너와 서비스를 사용할 수 있습니다.
