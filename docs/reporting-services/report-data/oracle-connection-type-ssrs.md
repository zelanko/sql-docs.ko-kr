---
title: "Oracle 연결 유형 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4ce6a83437433c2254b2993f68f78e8c8c8f4375
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="oracle-connection-type-ssrs"></a>Oracle 연결 형식(SSRS)
보고서에서 Oracle 데이터베이스의 데이터를 사용하려면 Oracle 유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 직접 Oracle 데이터 공급자를 사용 하 고 Oracle 클라이언트 소프트웨어 구성 요소가 필요 합니다.

Oracle 클라이언트 도구를 설치 하려면 다음을 수행할 수 있습니다.
 
1.  로 이동 [Oracle의 다운로드 사이트](http://www.oracle.com/us/products/tools/index-090165.html)
2.  Windows (서버에 대 한 64 비트, 도구에 대 한 32 비트) 용 ODAC 12c 릴리스 4 (12.1.0.2.4)를 다운로드 합니다.
3.  .NET 4에 대 한 데이터 공급자 설치
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)유형의 보고서 데이터 원본에 기초하는 데이터 집합이 있어야 합니다.  
  
##  <a name="Connection"></a> 연결 문자열  
 데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 유니코드를 사용하는 "Oracle9"라는 서버의 Oracle 데이터베이스를 지정합니다. 서버 이름은 Tnsnames.ora 구성 파일에 Oracle 서버 인스턴스 이름으로 정의되어 있는 이름과 일치해야 합니다.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 연결 문자열 예제에 대한 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
  
##  <a name="Query"></a> 쿼리  
 데이터 집합을 만들려면 드롭다운 목록에서 저장 프로시저를 선택하거나 SQL 쿼리를 만듭니다. 쿼리를 만들려면 텍스트 기반 쿼리 디자이너를 사용해야 합니다. 자세한 내용은 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
 결과 집합을 하나만 반환하는 저장 프로시저를 지정할 수 있습니다. 커서 기반 쿼리는 사용할 수 없습니다.  
  
##  <a name="Parameters"></a> 매개 변수  
 쿼리에 쿼리 변수가 포함된 경우 해당 보고서 매개 변수가 자동으로 생성됩니다. 이 확장 프로그램은 명명된 매개 변수를 지원합니다. Oracle 버전 9 이상의 경우 다중값 매개 변수가 지원됩니다.  
  
 보고서 매개 변수는 수정해야 할 수도 있는 기본 속성 값을 사용하여 만들어집니다. 예를 들어 각 보고서 매개 변수의 데이터 형식은 **Text**입니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다.  
  
  
##  <a name="Remarks"></a> 주의  
 Oracle 데이터 원본을 연결하려면 시스템 관리자가 Oracle 데이터베이스에서 데이터를 검색할 수 있도록 하는 .NET Data Provider for Oracle 버전을 설치해야 합니다. 이 데이터 공급자는 보고서 작성기와 동일한 컴퓨터뿐 아니라 보고서 서버에도 설치되어야 합니다.  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   msdn.microsoft.com의[.NET Framework Data Provider for Oracle 사용](http://go.microsoft.com/fwlink/?LinkId=112314)   
  
-   [Reporting Services를 사용한 Oracle 데이터 원본 구성 및 액세스 방법](http://support.microsoft.com/kb/834305)  
  
-   [NETWORK SERVICE 보안 주체에 대한 사용 권한을 추가하는 방법](http://support.microsoft.com/kb/870668)  
  
###### <a name="alternate-data-extensions"></a>대체 데이터 확장 프로그램  
 OLE DB 데이터 원본 유형을 사용하여 Oracle 데이터베이스에서 데이터를 검색할 수도 있습니다. 자세한 내용은 [OLE DB 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)을 참조하세요.  
  
###### <a name="report-models"></a>보고서 모델  
 Oracle 데이터베이스를 기반으로 모델을 만들 수도 있습니다.  
  
###### <a name="platform-and-version-information"></a>플랫폼 및 버전 정보  
 플랫폼 및 버전 지원에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

