---
title: 지원 되는 데이터 원본 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 52aae6defa5817236c4298d7c8e4cb44361a8284
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371315"
---
# <a name="data-sources-supported-ssas-tabular"></a>지원되는 데이터 원본 (SSAS 테이블 형식)
  이 항목에서는 테이블 형식 모델에서 사용할 수 있는 데이터 원본의 유형에 대해 설명합니다.  
  
 이 문서에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [지원되는 데이터 원본](#bkmk_supported_ds)  
  
-   [지원 되지 않는 원본](#bkmk_unsupported_ds)  
  
-   [데이터 원본 선택 시 유용한 정보](#bkmk_tips)  
  
##  <a name="bkmk_supported_ds"></a> 지원되는 데이터 원본  
 다음 표에 나와 있는 데이터 원본에서 데이터를 가져올 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 설치할 경우 각 데이터 원본에 대해 나열된 공급자는 설치되지 않습니다. 일부 공급자는 컴퓨터의 다른 애플리케이션과 함께 이미 설치되어 있을 수 있습니다. 그렇지 않은 경우에는 공급자를 다운로드하여 설치해야 합니다.  
  
|||||  
|-|-|-|-|  
|원본|버전|파일 유형|공급자 <sup>1</sup>|  
|Access 데이터베이스|Microsoft Access 2003, 2007, 2010|.accdb 또는 .mdb|ACE 14 OLE DB 공급자|  
|SQL Server 관계형 데이터베이스|Microsoft SQL Server2005, 2008, 2008 R2 SQL Server 2012, Microsoft SQL Azure 데이터베이스 <sup>2</sup>|(해당 사항 없음)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 공급자<br /><br /> SQL Server Native 10.0 Client OLE DB 공급자<br /><br /> .NET Framework Data Provider for SQL Client|  
|SQL Server 병렬 데이터 웨어하우스 (PDW) <sup>3</sup>|2008 R2|(해당 사항 없음)|SQL Server PDW용 OLE DB 공급자|  
|Oracle 관계형 데이터베이스|Oracle 9i, 10g, 11g|(해당 사항 없음)|Oracle OLE DB 공급자<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 관계형 데이터베이스|Teradata V2R6, V12|(해당 사항 없음)|TDOLEDB OLE DB 공급자<br /><br /> .Net Data Provider for Teradata|  
|Informix 관계형 데이터베이스||(해당 사항 없음)|Informix OLE DB 공급자|  
|IBM DB2 관계형 데이터베이스|8.1|(해당 사항 없음)|DB2OLEDB|  
|Sybase 적응형 Server Enterprise (ASE) 관계형 데이터베이스|15.0.2|(해당 사항 없음)|Sybase OLE DB 공급자|  
|기타 관계형 데이터베이스|(해당 사항 없음)|(해당 사항 없음)|OLE DB 공급자 또는 ODBC 드라이버|  
|텍스트 파일|(해당 사항 없음)|.txt, .tab, .csv|ACE 14 OLE DB provider for Microsoft Access|  
|Microsoft Excel 파일|Excel 97-2003, 2007, 2010|.xlsx, xlsm, .xlsb, .xltx, .xltm|ACE 14 OLE DB 공급자|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서(workbook)|Microsoft SQL Server 2008 R2 Analysis Services|.xlsx, xlsm, .xlsb, .xltx, .xltm|ASOLEDB 10.5<br /><br /> ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 가 설치된 SharePoint 팜에 게시된 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 통합 문서에만 사용)|  
|Analysis Services 큐브|Microsoft SQL Server 2005, 2008, 2008 R2 Analysis Services|(해당 사항 없음)|ASOLEDB 10|  
|데이터 피드<br /><br /> (Reporting Services 보고서, Atom 서비스 문서, Microsoft Azure Marketplace DataMarket 및 단일 데이터 피드에서 데이터를 가져오는 데 사용됨)|Atom 1.0 형식<br /><br /> 모든 데이터베이스 또는 WCF(Windows Communication Foundation) 데이터 서비스(이전 ADO.NET Data Services)로 노출되는 문서입니다.|하나 이상의 피드를 정의하는 서비스 문서용 .atomsvc<br /><br /> Atom 웹 피드 문서용 .atom|Microsoft Data Feed Provider for [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework 데이터 피드 데이터 공급자 - [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 데이터베이스 연결 파일||.odc||  
  
 <sup>1</sup> ODBC 용 OLE DB Provider를 사용할 수도 있습니다.  
  
 <sup>2</sup> SQL Azure 대 한 자세한 내용은 웹 사이트를 참조 하세요. [SQL Azure](https://go.microsoft.com/fwlink/?LinkID=157856)합니다.  
  
 <sup>3</sup> SQL Server PDW에 대 한 자세한 내용은 웹 사이트를 참조 하세요. [SQL Server 2008 R2 병렬 데이터 웨어하우스](https://go.microsoft.com/fwlink/?LinkId=150895)합니다.  
  
 <sup>4</sup> 일부 경우에 특히 최신 버전의 Oracle 사용 하 여 연결 오류가 발생할 수 있습니다 MSDAORA OLE DB 공급자를 사용 하 여 합니다. 오류가 발생할 경우 Oracle용으로 제시된 다른 공급자 중 하나를 사용해 보세요.  
  
##  <a name="bkmk_unsupported_ds"></a> 지원 되지 않는 원본  
 다음 데이터 원본은 현재 지원되지 않습니다.  
  
-   이미 SharePoint에 게시된 Access 데이터베이스와 같은 서버 문서는 가져올 수 없습니다.  
  
##  <a name="bkmk_tips"></a> 데이터 원본 선택 시 유용한 정보  
  
1.  모델 디자이너에서 테이블 간의 관계를 만들기 위해 가져오기를 수행하는 동안 *외래 키* 관계를 사용하기 때문에 관계형 데이터베이스에서 테이블을 가져오면 작업 단계가 줄어듭니다.  
  
2.  여러 테이블을 가져온 다음 필요 없는 테이블을 삭제하여 작업 단계를 줄일 수도 있습니다. 테이블을 한 번에 하나씩 가져오는 경우 테이블 간의 관계를 수동으로 만들어야 할 수 있습니다.  
  
3.  여러 데이터 원본의 유사 데이터를 포함하는 열은 모델 디자이너에서 관계를 만들 때 기반이 됩니다. 다른 유형의 데이터 원본을 사용하는 경우 동일하거나 비슷한 데이터가 포함되어 있는 다른 데이터 원본의 테이블에 매핑할 수 있는 열이 있는 테이블을 선택하십시오.  
  
4.  OLE DB 공급자는 경우에 따라 대량 데이터를 위해 더욱 빠른 성능을 제공할 수도 있습니다. 동일한 데이터 원본에 대해 여러 공급자 중에서 하나를 선택하는 경우 OLE DB 공급자를 먼저 사용해 보는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본&#40;SSAS 테이블 형식&#41;](../data-sources-ssas-tabular.md)   
 [데이터 가져오기&#40;SSAS 테이블 형식&#41;](../import-data-ssas-tabular.md)  
  
  
