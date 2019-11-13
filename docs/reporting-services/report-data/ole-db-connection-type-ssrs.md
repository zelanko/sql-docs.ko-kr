---
title: OLE DB 연결 형식(SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a00f7dc1d38f687f2a21c7ba7bf07e41987beee1
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593969"
---
# <a name="ole-db-connection-type-ssrs"></a>OLE DB 연결 형식(SSRS)
  OLE DB 데이터 공급자의 데이터를 포함하려면 OLE DB 유형의 보고서 데이터 원본에 기초하는 데이터 세트가 있어야 합니다. 이 기본 제공 데이터 원본 유형은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] OLE DB 데이터 처리 확장 프로그램을 기반으로 합니다.  
  
 OLE DB는 클라이언트가 다양한 데이터 공급자에 연결할 수 있도록 하는 데이터 액세스 기술입니다. 데이터 원본 유형 OLE DB를 선택한 후에는 특정 데이터 공급자를 선택해야 합니다. 매개 변수 및 자격 증명과 같은 기능에 대한 지원은 선택하는 데이터 공급자에 따라 달라집니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Connection"></a> 연결 문자열  
 OLE DB 데이터 처리 확장 프로그램의 연결 문자열은 원하는 데이터 공급자에 따라 달라집니다. 일반적인 연결 문자열에는 데이터 공급자가 지원하는 이름/값 쌍이 포함됩니다. 예를 들어 다음 연결 문자열은 OLE DB provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 및 AdventureWorks 데이터베이스를 지정합니다.  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 사용하는 연결 문자열은 연결하려는 외부 데이터 원본에 따라 달라집니다. 데이터 공급자별 연결 문자열 속성을 설정하려면 **데이터 원본 속성** 대화 상자의 **일반** 페이지에서 **빌드** 단추를 클릭하여 **연결 속성** 대화 상자를 엽니다. **데이터 연결 속성** 대화 상자를 통해 확장된 데이터 원본 속성을 설정합니다.  
  
 연결 문자열의 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 &#40;문자열 보고서 작성기 및 SSRS&#41; ](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 데이터 원본에 대 한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)을 참조 하세요.  
  
###### <a name="special-characters-in-a-password"></a>암호의 특수 문자  
 암호를 입력하라는 메시지를 표시하거나 연결 문자열에 암호를 포함하도록 OLE DB 데이터 원본을 구성한 경우 사용자가 문장 부호와 같은 특수 문자가 포함된 암호를 입력하면 일부 기본 데이터 원본 드라이버에서 해당 특수 문자의 유효성을 검사할 수 없습니다. 보고서 처리 시 "올바른 암호가 아닙니다" 메시지가 나타나면 이 문제 때문일 수 있습니다.  
  
> [!NOTE]  
>  연결 문자열에 암호와 같은 로그인 정보를 추가하지 않는 것이 좋습니다. 보고서 작성기는 **데이터 원본** 대화 상자에서 자격 증명을 입력하는 데 사용할 수 있는 별도의 탭을 제공합니다.  
  
  
##  <a name="Parameters"></a> 매개 변수  
 일부 OLE DB 공급자는 명명되지 않은 매개 변수 및 이름이 지정되지 않은 매개 변수를 지원합니다. 매개 변수는 쿼리의 자리 표시자를 사용하여 위치로 전달됩니다. 자리 표시자 문자는 데이터 공급자가 지원하는 구문에 따라 결정됩니다.  
  
  
##  <a name="Remarks"></a> 주의  
 OLEDB는 특정 데이터 원본에 사용할 데이터 공급자를 만들기 위한 기본 기술입니다. OLEDB는 COM(구성 요소 개체 모델) 인터페이스를 기반으로 합니다. OLEDB는 ODBC보다 뒤에 나오고 ADO.NET 데이터 공급자 이전에 나온 기술입니다. OLEDB 공급자는 다른 모든 COM 구성 요소와 마찬가지로 운영 체제에 등록됩니다. OLEDB 데이터 공급자는 Microsoft 및 타사 공급업체를 통해 사용할 수 있습니다. Microsoft는 ODBC 드라이버에 대한 통신을 연결하는 OLEDB 데이터 공급자인 MSDASQL도 제공합니다. 자세한 내용은 [ODBC 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)을 참조하세요.  
  
 원하는 데이터를 성공적으로 검색하려면 데이터 공급자가 지원하는 쿼리 구문을 제공해야 합니다. 매개 변수 지원은 데이터 공급자에 따라 다릅니다. 자세한 내용은 선택한 데이터 공급자와 관련된 항목을 참조하십시오. 예를 들어  
  
-   [Analysis Services OLE DB 공급자&#40;Analysis Services - 다차원 데이터&#41;](https://docs.microsoft.com/analysis-services/instances/data-providers-used-for-analysis-services-connections
)  
   
  
-   [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 특정 OLE DB 데이터 공급자에 대한 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 세트를 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 세트 또는 포함된 데이터 세트 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 세트에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 세트&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 세트 및 공유 데이터 세트에 대한 정보를 제공합니다.  
  
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 세트 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
