---
title: "지원 되는 데이터 원본 (SSAS-다차원) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2089ceaf95022e1bed0e7409d9ccbc4af3a64fba
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="supported-data-sources-ssas---multidimensional"></a>지원되는 데이터 원본(SSAS - 다차원)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
이 항목에서는 다차원 모델에서 사용할 수 있는 데이터 원본 유형에 대해 설명합니다.  
  
##  <a name="bkmk_supported_ds"></a> 지원되는 데이터 원본  
 다음 표에 나와 있는 데이터 원본에서 데이터를 검색할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 설치할 경우 각 데이터 원본에 대해 나열된 공급자는 설치되지 않습니다. 일부 공급자는 컴퓨터의 다른 응용 프로그램과 함께 이미 설치되어 있을 수 있습니다. 그렇지 않은 경우에는 공급자를 다운로드하여 설치해야 합니다.  
  
> [!NOTE]  
>  Oracle OLE DB 공급자와 같은 타사 공급자를 사용하여 타사에서 제공하는 지원을 통해 타사 데이터베이스에 연결할 수도 있습니다.  
  
|||||  
|-|-|-|-|  
|원본|버전|파일 유형|공급자*|  
|Access 데이터베이스|Microsoft Access 2010, 2013, 2016|.accdb 또는 .mdb|Microsoft Jet 4.0 OLE DB Provider|  
|SQL Server 관계형 데이터베이스*|Microsoft SQL Server 2008, 2008 R2, 2012, 2014, 2016, [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)], Azure SQL 데이터 웨어하우스, Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> 참고: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 자세한 내용은 [Azure.com](http://go.microsoft.com/fwlink/?LinkID=157856)을 참조하세요.<br /><br /> 참고: Analytics Platform System (APS)의 이전 명칭은 SQL Server 병렬 데이터 웨어하우스 (PDW). 원래는 PDW에서 Analysis Services에 연결하려면 특수한 데이터 공급자가 필요했습니다. 이 공급자는 SQL Server 2012에서 바뀌었습니다. SQL Server 2012부터는 PDW/APS에 대한 연결에 SQL Server Native Client가 사용됩니다. APS에 대한 자세한 내용은 [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx)웹 사이트를 참조하세요.|(해당 사항 없음)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 공급자<br /><br /> SQL Server Native 11.0 Client OLE DB 공급자<br /><br /> .NET Framework Data Provider for SQL Client|  
|Oracle 관계형 데이터베이스|Oracle 9i, 10g, 11g, 12g|(해당 사항 없음)|Oracle OLE DB 공급자<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 관계형 데이터베이스|Teradata V2R6, V12|(해당 사항 없음)|TDOLEDB OLE DB 공급자<br /><br /> .Net Data Provider for Teradata|  
|Informix 관계형 데이터베이스|V11.10|(해당 사항 없음)|Informix OLE DB 공급자|  
|IBM DB2 관계형 데이터베이스|8.1|(해당 사항 없음)|DB2OLEDB|  
|Sybase 적응형 Server Enterprise (ASE) 관계형 데이터베이스|15.0.2|(해당 사항 없음)|Sybase OLE DB 공급자|  
|기타 관계형 데이터베이스|(해당 사항 없음)|(해당 사항 없음)|OLE DB Provider|  
  
 \* ODBC 데이터 원본은 다차원 솔루션에서 지원되지 않습니다. Analysis Services 자체는 연결을 처리하지만 솔루션을 빌드하는 데 사용되는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 디자이너는 MSDASQL 드라이버를 사용하는 경우에도 ODBC 데이터 원본에 연결할 수 없습니다. 비즈니스 요구 사항에 ODBC 데이터 원본이 포함되는 경우 테이블 형식 솔루션을 대신 빌드해 보세요.  
  
 ** 일부 기능의 경우 온-프레미스로 실행되는 SQL Server 관계형 데이터베이스가 필요합니다. 특히 쓰기 저장 및 ROLAP 저장소를 사용하려면 기본 데이터 원본이 SQL Server 관계형 데이터베이스여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [지원 되는 데이터 원본](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [다차원 모델의 데이터 원본](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
