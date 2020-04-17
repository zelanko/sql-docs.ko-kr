---
title: SSIS, MDS 및 DQS를 함께 사용하는 엔터프라이즈 정보 관리 [자습서] | 마이크로 소프트 문서
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487722"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>SSIS, MDS 및 DQS를 함께 사용하는 엔터프라이즈 정보 관리 [자습서]
  기업의 정보 관리에는 일반적으로 기업 내부 및 외부의 데이터를 통합하고, 데이터를 정리하고, 데이터를 비교해서 중복 항목을 제거하고, 데이터를 표준화하고, 데이터를 강화하고, 데이터에 대한 법적 및 컴플라이언스 요구 사항을 준수하고, 모든 필수 보안 설정을 사용해서 데이터를 중앙 위치에 저장하는 모든 과정이 포함됩니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 단일 제품으로 효과적인 EIM(엔터프라이즈 정보 관리) 솔루션을 제공하기 위해 필요한 모든 구성 요소를 제공합니다. EIM 솔루션을 구축하는 데 도움이 되는 핵심 구성 요소는 다음과 같습니다.  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SSIS(SQL Server Integration Services)는 다양한 원본의 데이터를 비즈니스 워크플로, 데이터 웨어하우스 또는 마스터 데이터 관리가 지원되는 포괄적인 ETL(추출, 변환 및 로드) 솔루션으로 통합하기 위한 강력하고 확장 가능한 플랫폼을 제공합니다. SSIS의 간략한 개요 및 일반적인 용도는 [통합 서비스 개요](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) 항목을 참조하십시오.  
  
 SQL Server DQS(Data Quality Services)를 사용하면 비즈니스 인텔리전스, 데이터 웨어하우스 및 트랜잭션 처리 작업을 위해 신뢰할 수 있는 정보를 제공할 수 있도록 데이터를 정리, 일치, 표준화 및 강화할 수 있습니다. DQS에 대한 비즈니스 요구 사항 및 DQS가 요구에 [응답하는](https://msdn.microsoft.com/library/ff877917.aspx) 방법에 대한 데이터 품질 서비스 소개 항목을 참조하십시오.  
  
 SQL Server MDS(Master Data Services)는 정보 무결성 및 데이터 일관성이 여러 애플리케이션 간에 일관되게 유지되도록 보장하는 중앙 데이터 허브를 제공합니다. MDS의 주요 기능에 대한 간략한 설명은 [마스터 데이터 서비스 개요](../master-data-services/master-data-services-overview-mds.md) 항목을 참조하십시오.  
  
 EIM Technologies 백서를 [사용하여 마스터 데이터 정리 및 일치를](https://msdn.microsoft.com/library/hh403491.aspx) 참조하여 이러한 Microsoft EIM 기술을 함께 사용하여 EIM 솔루션을 구현하는 방법에 대한 포괄적인 지침을 확인하고 [EIM(엔터프라이즈 정보 관리) : SSIS, DQS 및 MDS](https://go.microsoft.com/fwlink/?LinkId=258672) 비디오를 함께 가져와 EIM 시나리오를 멋지게 시연합니다.  
  
 이 자습서에서는 SSIS, MDS 및 DQS 기술을 함께 활용해서 예제 EIM(엔터프라이즈 정보 관리) 솔루션을 구현하는 방법에 대해 알아봅니다. 먼저, DQS를 사용해서 데이터(메타데이터)에 대한 지식이 포함된 기술 자료를 만들고, 기술 자료를 사용해서 Excel 파일에서 데이터를 정리하고, 데이터 일치를 통해 데이터에 있는 중복 항목을 식별 및 제거합니다. 그런 다음 Excel용 MDS 추가 기능을 사용해서 정리되고 일치된 데이터를 MDS에 업로드합니다. 마지막으로 SSIS 솔루션을 사용해서 전체 프로세스를 자동화합니다. 이 자습서의 SSIS 솔루션은 Excel 파일에서 입력 데이터를 읽지만 오라클, 테라데이타, DB2 및 Azure SQL Database와 같은 다양한 소스에서 읽도록 확장할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
1.  다음 구성 요소가 설치된 Microsoft SQL Server 2012가 필요합니다.  
  
    1.  Integration Services(SSIS)  
  
    2.  MDS(Master Data Services)  
  
    3.  DQS(Data Quality Services)  
  
    4.  SQL Server Data Tools  
  
         제품 설치에 대한 자세한 내용은 [SQL Server 2012 설치 가이드를](../database-engine/install-windows/installation-for-sql-server.md) 참조하십시오.  
  
2.  [Master Data Services 구성 마법사를 사용하여 MDS를 구성합니다.](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     구성 관리자를 사용하여 MDS(Master Data Services) 데이터베이스를 만들고 구성할 수 있습니다. MDS 데이터베이스를 만든 후 웹 사이트에서 MDS용 웹 응용 프로그램을 `http://localhost/MDS`만들고(예: ) MDS 데이터베이스를 MDS 웹 응용 프로그램과 연결합니다. MDS 웹 애플리케이션을 만들려면 컴퓨터에 IIS가 설치되어 있어야 합니다. MDS 데이터베이스 및 웹 응용 프로그램을 구성하기 위한 필수 구성 조건에 대한 자세한 내용은 [웹 응용 프로그램 요구 사항(마스터 데이터 서비스)](https://msdn.microsoft.com/library/ee633744.aspx) 및 데이터베이스 요구 [사항(마스터 데이터 서비스)을](https://msdn.microsoft.com/library/ee633767.aspx) 참조하십시오.  
  
3.  [데이터 품질 서버 설치 관리자를 사용하여 DQS를 설치하고 구성합니다.](https://msdn.microsoft.com/library/hh231682.aspx) **시작을**클릭하고 **모든 프로그램을**클릭하고 Microsoft SQL Server **2014를**클릭하고 **데이터 품질 서비스를**클릭한 다음 데이터 품질 서버 **설치 관리자를**클릭합니다.  
  
4.  Microsoft Excel 2010(32비트 선호)이 필요합니다.  
  
5.  [여기에서](https://www.microsoft.com/download/details.aspx?id=29064) **Excel에 대한 마스터 데이터 서비스 추가 기능** 설치(컴퓨터에 있는 Excel 버전에 따라 32비트 또는 64비트). 컴퓨터에 설치된 Excel 버전을 찾으려면 **Excel을**실행하고 메뉴 모음에서 **파일을** 클릭하고 **도움말을** 클릭하여 오른쪽 창에서 버전을 확인합니다. Excel 추가 기능을 설치하려면 먼저 Visual Studio 2010 Tools for Office Runtime을 설치해야 합니다.  
  
6.  (선택 사항) [Azure 마켓플레이스를](https://azuremarketplace.microsoft.com/marketplace/)사용하여 계정을 만듭니다. 이 자습서에서 수행하는 작업 중 하나에서는 **Azure Marketplace**(원래 이름은 **데이터 마켓**) 계정이 필요합니다. 필요에 따라 이 작업을 건너뛰고 다음 작업을 진행할 수 있습니다.  
  
7.  [Microsoft 다운로드 센터에서](https://www.microsoft.com/download/details.aspx?id=50426)Suppliers.xls 파일을 다운로드합니다.  
  
8.  **64비트 버전의 Excel을**사용하는 경우 DQS에서 정리 또는 일치하는 결과를 Excel 파일로 내보낼 수 없습니다. 이 문제는 알려진 문제입니다. 이 문제를 해결하려면 다음을 수행하십시오.  
  
    1.  **실행 DQLInstaller.exe -업그레이드**. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn에 있습니다. DQSInstaller.exe 파일을 두 번 클릭합니다.  
  
    2.  **마스터 데이터 서비스 구성 관리자에서**데이터베이스 **선택을**클릭하고 기존 **MDS** 데이터베이스를 선택한 다음 **업그레이드**를 클릭합니다.  
  
## <a name="lessons"></a>단원  
  
|단원|간단한 설명|소요되는 예상 시간(분)|  
|------------|-----------------------|------------------------------------------------|  
|[1단원: 공급자 DQS 기술 자료 만들기](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|이 단원에서는 공급자라는 DQS 기술 **자료가 작성됩니다.**|60|  
|[2단원: 공급자 기술 자료를 사용하여 공급자 데이터 정리](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|이 단원에서는 첫 번째 단원에서 만든 공급자 기술 자료를 사용하여 Excel 파일에서 **공급자** 데이터를 정리하기 위해 DQS 프로젝트를 만들고 실행합니다.|45|  
|[3단원: 데이터 일치로 공급자 목록에서 중복 항목 제거](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|이 단원에서는 정리된 공급자 목록에서 중복 항목을 식별하고 제거하는 일치 작업을 수행하기 위해 DQS 프로젝트를 만듭니다.|45|  
|[4단원: MDS에 공급자 데이터 저장](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|이 단원에서는 **Excel용 MDS 추가 기능을**사용하여 정리되고 일치하는 공급자 데이터를 MDS(마스터 데이터 서비스)에 업로드합니다.|45|  
|[5단원: SSIS를 사용하여 정리 및 일치 자동화](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|이 단원에서는 DQS를 사용해서 입력 데이터를 정리하고, 정리된 데이터를 비교해서 중복 항목을 제거하고, MDS에서 정리 및 일치된 데이터를 자동화된 방식으로 저장하는 SSIS 솔루션을 만듭니다.|75|  
  
## <a name="next-steps"></a>다음 단계  
 자습서를 시작하려면 첫 번째 [단원: 1과: 공급업체 DQS 기술 자료 만들기.](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)  
  
  
