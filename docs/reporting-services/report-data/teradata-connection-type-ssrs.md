---
title: Teradata 연결 형식(SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 473ddb100476b3b25af3141a2d56c073648f170b
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029872"
---
# <a name="teradata-connection-type-ssrs"></a>Teradata 연결 형식(SSRS)
  보고서에 Teradata 관계형 데이터베이스의 데이터를 포함하려면 Teradata 유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 .NET Managed Provider for Teradata 데이터 처리 확장 프로그램을 기반으로 합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Connection"></a> 연결 문자열  
 데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 유니코드를 사용하는 IP 주소로 지정된 서버의 Teradata 데이터베이스를 지정합니다.  
  
```  
data source=<IP Address>  
```  
  
 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 작성기에 자격 증명 지정](https://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
  
##  <a name="Remarks"></a> 주의  
 Teradata 데이터 원본을 연결하려면 시스템 관리자가 Teradata 데이터베이스에서 데이터를 검색할 수 있도록 하는 .NET Data Provider for Teradata 버전을 설치해야 합니다. 이 데이터 공급자는 보고서 작성기와 동일한 컴퓨터뿐 아니라 보고서 서버에도 설치되어야 합니다.  
  
 이 데이터 공급자는 일부 보고서 배달 모드만 지원합니다. 이 데이터 처리 확장 프로그램에서는 데이터 기반 구독을 통한 보고서 배달이 지원되지 않습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)을 참조하세요.  
  
  
##  <a name="Models"></a> 보고서 모델  
 Teradata 데이터 원본에 기반을 둔 보고서 모델에서 데이터 집합을 만들려면 모델이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 모델 디자이너에서 디자인되어 보고서 서버에 게시되어 있어야 합니다.  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 데이터 집합 쿼리에 의해 생성되는 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?linkid=121312)에 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
 [.NET Framework Data Provider for Teradata에서 SQL Server 2008 Reporting Services 사용](https://go.microsoft.com/fwlink/?LinkID=130848)  
 이 데이터 확장 프로그램을 사용하는 방법에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
