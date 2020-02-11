---
title: SSIS, MDS 및 DQS를 함께 사용 하는 엔터프라이즈 정보 관리 [자습서] | Microsoft Docs
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
ms.openlocfilehash: 47bb74bf5fd35696481a88c4ccc30a8733f257a2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153558"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>SSIS, MDS 및 DQS를 함께 사용하는 엔터프라이즈 정보 관리 [자습서]
  기업의 정보 관리에는 일반적으로 기업 내부 및 외부의 데이터를 통합하고, 데이터를 정리하고, 데이터를 비교해서 중복 항목을 제거하고, 데이터를 표준화하고, 데이터를 강화하고, 데이터에 대한 법적 및 컴플라이언스 요구 사항을 준수하고, 모든 필수 보안 설정을 사용해서 데이터를 중앙 위치에 저장하는 모든 과정이 포함됩니다.  
  
 
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 단일 제품으로 효과적인 EIM(엔터프라이즈 정보 관리) 솔루션을 제공하기 위해 필요한 모든 구성 요소를 제공합니다. EIM 솔루션을 구축하는 데 도움이 되는 핵심 구성 요소는 다음과 같습니다.  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SSIS(SQL Server Integration Services)는 다양한 원본의 데이터를 비즈니스 워크플로, 데이터 웨어하우스 또는 마스터 데이터 관리가 지원되는 포괄적인 ETL(추출, 변환 및 로드) 솔루션으로 통합하기 위한 강력하고 확장 가능한 플랫폼을 제공합니다. SSIS의 빠른 개요 및 일반적인 사용은 [Integration Services 개요](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) 항목을 참조 하세요.  
  
 SQL Server DQS(Data Quality Services)를 사용하면 비즈니스 인텔리전스, 데이터 웨어하우스 및 트랜잭션 처리 작업을 위해 신뢰할 수 있는 정보를 제공할 수 있도록 데이터를 정리, 일치, 표준화 및 강화할 수 있습니다. DQS의 비즈니스 요구에 대 한 [데이터 품질 서비스 소개](https://msdn.microsoft.com/library/ff877917.aspx) 항목과 dqs의 요구 사항을 확인 하는 방법을 참조 하세요.  
  
 SQL Server MDS(Master Data Services)는 정보 무결성 및 데이터 일관성이 여러 애플리케이션 간에 일관되게 유지되도록 보장하는 중앙 데이터 허브를 제공합니다. MDS의 중요 한 기능에 대 한 간략 한 설명은 [MDS(Master Data Services) 개요](../master-data-services/master-data-services-overview-mds.md) 항목을 참조 하세요.  
  
 이러한 Microsoft EIM 기술을 함께 사용 하 여 EIM 솔루션을 구현 하는 방법에 대 한 포괄적인 지침을 보려면 [Eim 기술을 사용 하 여 마스터 데이터 정리 및 일치](https://msdn.microsoft.com/library/hh403491.aspx) 백서를 참조 하 고 [Eim (엔터프라이즈 정보 관리): SSIS, DQS 및 MDS](https://go.microsoft.com/fwlink/?LinkId=258672) 비디오를 통합 하 여 eim 시나리오의 유용한 데모를 시청 하세요.  
  
 이 자습서에서는 SSIS, MDS 및 DQS 기술을 함께 활용해서 예제 EIM(엔터프라이즈 정보 관리) 솔루션을 구현하는 방법에 대해 알아봅니다. 먼저, DQS를 사용해서 데이터(메타데이터)에 대한 지식이 포함된 기술 자료를 만들고, 기술 자료를 사용해서 Excel 파일에서 데이터를 정리하고, 데이터 일치를 통해 데이터에 있는 중복 항목을 식별 및 제거합니다. 그런 다음 Excel용 MDS 추가 기능을 사용해서 정리되고 일치된 데이터를 MDS에 업로드합니다. 마지막으로 SSIS 솔루션을 사용해서 전체 프로세스를 자동화합니다. 이 자습서의 SSIS 솔루션은 Excel 파일에서 입력 데이터를 읽지만 Oracle, Teradata, DB2 및 Azure SQL Database 같은 다양 한 원본에서 데이터를 읽도록 확장할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
1.  다음 구성 요소가 설치된 Microsoft SQL Server 2012가 필요합니다.  
  
    1.  Integration Services(SSIS)  
  
    2.  MDS(Master Data Services)  
  
    3.  DQS(Data Quality Services)  
  
    4.  SQL Server Data Tools  
  
         제품을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server 2012 설치 가이드](../database-engine/install-windows/installation-for-sql-server.md) 를 참조 하세요.  
  
2.  [Master Data Services 구성 마법사를 사용하여 MDS를 구성합니다.](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     구성 관리자를 사용하여 MDS(Master Data Services) 데이터베이스를 만들고 구성할 수 있습니다. MDS 데이터베이스를 만든 후 웹 사이트 (예: [http://localhost/MDS](http://localhost/MDS))에서 mds에 대 한 웹 응용 프로그램을 만들고 mds 데이터베이스를 mds 웹 응용 프로그램에 연결 합니다. MDS 웹 애플리케이션을 만들려면 컴퓨터에 IIS가 설치되어 있어야 합니다. MDS 데이터베이스 및 웹 응용 프로그램을 구성 하기 위한 필수 구성 요소에 대 한 자세한 내용은 [웹 응용 프로그램 요구 사항 (MDS(Master Data Services))](https://msdn.microsoft.com/library/ee633744.aspx) 및 [데이터베이스 요구 사항 (MDS(Master Data Services))](https://msdn.microsoft.com/library/ee633767.aspx) 을 참조 하십시오.  
  
3.  [Data Quality 서버 설치 관리자를 사용 하 여 DQS를 설치 하 고 구성](https://msdn.microsoft.com/library/hh231682.aspx)합니다. **시작**, **모든 프로그램**, **Microsoft SQL Server 2014**, **Data Quality Services**, **data quality 서버 설치 프로그램**을 차례로 클릭 합니다.  
  
4.  Microsoft Excel 2010(32비트 선호)이 필요합니다.  
  
5.  [여기](https://www.microsoft.com/download/details.aspx?id=29064)에서 **Excel용 Master Data Services 추가 기능** (컴퓨터에 있는 Excel 버전에 따라 32 비트 또는 64 비트)를 설치 합니다. 컴퓨터에 설치 된 Excel 버전을 찾으려면 **excel**을 실행 하 고 메뉴 모음에서 **파일** 을 클릭 한 다음 **도움말** 을 클릭 하 여 오른쪽 창에서 버전을 확인 합니다. Excel 추가 기능을 설치하려면 먼저 Visual Studio 2010 Tools for Office Runtime을 설치해야 합니다.  
  
6.  필드 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/)를 사용 하 여 계정을 만듭니다. 이 자습서에서 수행하는 작업 중 하나에서는 **Azure Marketplace**(원래 이름은 **데이터 마켓**) 계정이 필요합니다. 필요에 따라 이 작업을 건너뛰고 다음 작업을 진행할 수 있습니다.  
  
7.  [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50426)에서 Suppliers .xls 파일을 다운로드 합니다.  
  
8.  **64 비트 버전의 excel**을 사용 하는 경우 dqs를 사용 하 여 정리 또는 일치 결과를 excel 파일로 내보낼 수 없습니다. 이 문제는 알려진 문제입니다. 이 문제를 해결하려면 다음을 수행하십시오.  
  
    1.  **DQLInstaller-upgrade**를 실행 합니다. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn에 있습니다. DQSInstaller.exe 파일을 두 번 클릭합니다.  
  
    2.  **Master Data Services 구성 관리자**에서 **데이터베이스 선택**을 클릭 하 고 기존 **MDS** 데이터베이스를 선택한 다음 **업그레이드**를 클릭 합니다.  
  
## <a name="lessons"></a>단원  
  
|단원|간단한 설명|소요되는 예상 시간(분)|  
|------------|-----------------------|------------------------------------------------|  
|[1단원: 공급자 DQS 기술 자료 만들기](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|이 단원에서는 **Suppliers**라는 DQS 기술 자료를 만듭니다.|60|  
|[2단원: 공급자 기술 자료를 사용하여 공급자 데이터 정리](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|이 단원에서는 첫 번째 단원에서 만든 **Suppliers** 기술 자료를 사용 하 여 Excel 파일에서 공급자 데이터를 정리 하기 위해 DQS 프로젝트를 만들고 실행 합니다.|45|  
|[3단원: 데이터 일치로 공급자 목록에서 중복 항목 제거](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|이 단원에서는 정리된 공급자 목록에서 중복 항목을 식별하고 제거하는 일치 작업을 수행하기 위해 DQS 프로젝트를 만듭니다.|45|  
|[4단원: MDS에 공급자 데이터 저장](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|이 단원에서는 **Excel용 MDS 추가 기능**를 사용 하 여 정리 및 일치 된 공급자 데이터를 MDS (MDS(Master Data Services))에 업로드 합니다.|45|  
|[5단원: SSIS를 사용하여 정리 및 일치 자동화](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|이 단원에서는 DQS를 사용해서 입력 데이터를 정리하고, 정리된 데이터를 비교해서 중복 항목을 제거하고, MDS에서 정리 및 일치된 데이터를 자동화된 방식으로 저장하는 SSIS 솔루션을 만듭니다.|75|  
  
## <a name="next-steps"></a>다음 단계  
 자습서를 시작 하려면 첫 번째 단원인 [1 단원: SUPPLIERS DQS 기술 자료 만들기](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)를 계속 진행 합니다.  
  
  
