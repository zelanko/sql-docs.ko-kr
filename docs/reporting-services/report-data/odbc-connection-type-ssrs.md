---
title: "ODBC 연결 유형 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 24163866-f37a-4c38-982e-c3d79bf64d4c
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c72d825a49524ec97ac6cea5f59463f6b8b7d205
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="odbc-connection-type-ssrs"></a>ODBC 연결 형식(SSRS)
  ODBC 데이터 공급자의 데이터를 포함하려면 ODBC 유형의 보고서 데이터 원본에 기초하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ODBC 데이터 처리 확장 프로그램을 기반으로 합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)유형의 보고서 데이터 원본에 기초하는 데이터 집합이 있어야 합니다.  
  
##  <a name="Connection"></a> 연결 문자열  
 ODBC 데이터 처리 확장 프로그램의 연결 문자열은 원하는 ODBC 드라이버에 따라 달라집니다. 일반적인 연결 문자열에는 드라이버가 지원하는 이름/값 쌍이 포함됩니다. 예를 들어 다음 연결 문자열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 및 AdventureWorks 데이터베이스에 대한 ODBC 드라이버를 지정합니다.  
  
```  
Driver={SQL Server Native Client 10.0};Server=server;Database=AdventureWorks;Trusted_Connection=yes;  
```  
  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 암호를 입력하라는 메시지를 표시하거나 연결 문자열에 암호를 포함하도록 ODBC 데이터 원본을 구성한 경우 사용자가 문장 부호와 같은 특수 문자가 포함된 암호를 입력하면 일부 기본 데이터 원본 드라이버에서 해당 특수 문자의 유효성을 검사할 수 없습니다. 보고서 처리 시 "올바른 암호가 아닙니다" 메시지가 나타나면 이 문제 때문일 수 있습니다. 암호를 변경하는 것이 불가능한 경우 데이터베이스 관리자와 협력하여 보고서 서버에서 해당 자격 증명을 시스템 ODBC DSN(데이터 원본 이름)의 일부로 저장할 수 있습니다. 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서의 "OdbcConnection.ConnectionString"을 참조하세요.  
  
> [!NOTE]  
>  연결 문자열에 암호와 같은 로그인 정보를 추가하지 않는 것이 좋습니다. 보고서 작성기는 **데이터 원본** 대화 상자에서 자격 증명을 입력하는 데 사용할 수 있는 별도의 탭을 제공합니다.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
  
##  <a name="Remarks"></a> 주의  
 ODBC는 OLEDB에 앞서 도입된 초기 데이터 액세스 기술입니다. ODBC는 관계형 데이터 원본만 지원합니다. ODBC 데이터 공급자를 *드라이버*라고 합니다. ODBC 드라이버는 Microsoft 및 타사 공급업체가 제공합니다. 예를 들어 Microsoft Office는 Office 파일 형식에 연결되는 ODBC 드라이버를 설치합니다.  
  
 ODBC 연결 문자열을 작성할 수 있으려면 먼저 ODBC 드라이버가 설치되어 있고 컴퓨터 또는 시스템 DSN을 작성해야 합니다. 원하는 데이터를 성공적으로 검색하려면 드라이버가 지원하는 쿼리 구문을 제공해야 합니다. 매개 변수 지원은 드라이버에 따라 다릅니다. 자세한 내용은 선택한 드라이버와 관련된 항목을 참조하세요(예: [SQL Server Native Client&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)).  
  
###### <a name="platform-and-version-information"></a>플랫폼 및 버전 정보  
 특정 ODBC 데이터 공급자에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
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
  
  
