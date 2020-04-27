---
title: 데이터 가져오기 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7eb3fe1157ba40466cc619f504255084aa845fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080623"
---
# <a name="import-data-ssas-tabular"></a>데이터 가져오기(SSAS 테이블 형식)
  다양한 원본의 데이터를 테이블 형식 모델로 가져올 수 있습니다. 이 섹션의 항목에서는 데이터 가져오기 마법사를 사용하여 데이터를 가져올 모델 프로젝트에 연결하고 가져올 데이터를 선택하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  모델에 많은 행이 포함된 테이블이 있는 경우에는 모델 제작 중에 데이터의 하위 집합만 가져오는 것이 좋습니다. 데이터의 하위 집합을 가져오면 처리 시간 및 작업 영역 데이터베이스 서버 리소스 사용량을 줄일 수 있습니다.  
  
 테이블 가져오기 마법사를 사용하여 다음 데이터 원본에서 데이터를 가져올 수 있습니다.  
  
|**데이터 원본**|**설명**|  
|---------------------|---------------------|  
|**관계형 데이터베이스**|관계형 데이터 원본에는 다음이 포함됩니다.<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Microsoft SQL Server 병렬 데이터 웨어하우스<br /><br /> Microsoft Access<br /><br /> Oracle<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**다차원 원본**|Microsoft SQL Server Analysis Services 큐브|  
|**데이터 피드**|데이터 피드에는 다음이 포함됩니다.<br /><br /> Microsoft Reporting Services 보고서<br /><br /> Azure DataMarket 데이터 세트<br /><br /> 공개 공급자나 기업 공급자의 Atom 피드|  
|**텍스트 파일**|텍스트 파일에는 다음이 포함됩니다.<br /><br /> Excel 파일(.xlsx)<br /><br /> 텍스트 파일(.txt)|  
  
 테이블 가져오기 마법사를 사용하여 데이터를 가져올 수 있을 뿐 아니라, 클립보드에서 복사한 데이터를 테이블에 붙여넣을 수도 있습니다. 붙여넣은 데이터는 다른 데이터 원본에서 가져온 데이터와 다르게 동작합니다. 테이블에 붙여넣은 데이터에는 연결 이름이나 원본 데이터 속성이 없습니다. 붙여넣은 데이터는 Model.bim 파일에 보관됩니다. 프로젝트 또는 Model.bim 파일이 저장되면 붙여넣은 데이터도 저장됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|항목|설명|  
|-----------|-----------------|  
|[관계형 데이터 원본에서 가져오기 &#40;SSAS 테이블 형식&#41;](import-from-a-relational-data-source-ssas-tabular.md)|Microsoft SQL Server, Oracle, Teradata 데이터베이스 등의 관계형 데이터 원본에서 데이터를 가져오는 방법을 설명합니다.|  
|[다차원 데이터 원본에서 가져오기 &#40;SSAS 테이블 형식&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|다차원 SQL Server Analysis Services 큐브에서 데이터를 가져오는 방법을 설명합니다.|  
|[SSAS 테이블 형식&#41;&#40;데이터 피드에서 가져오기](import-from-a-data-feed-ssas-tabular.md)|Microsoft Reporting Services 보고서나 Azure Data Market 데이터 세트 등의 데이터 피드에서 데이터를 가져오는 방법을 설명합니다.|  
|[SSAS 테이블 형식&#41;&#40;텍스트 파일에서 가져오기](import-from-a-text-file-ssas-tabular.md)|Microsoft Excel 통합 문서 또는 텍스트 파일에서 데이터를 가져오는 방법을 설명합니다.|  
|[데이터 복사 및 붙여넣기&#40;SSAS 테이블 형식&#41;](copy-and-paste-data-ssas-tabular.md)|붙여넣기 및 추가하여 붙여넣기를 사용하여 모델 디자이너의 기존 테이블에 데이터를 추가하는 방법을 설명합니다.|  
  
  
