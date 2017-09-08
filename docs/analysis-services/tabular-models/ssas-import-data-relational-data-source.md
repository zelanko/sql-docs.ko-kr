---
title: "관계형 데이터 원본 (SSAS 테이블 형식)에서 가져오기 | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1db6dd24d059f8c478967bc3c69652aaec0aeb51
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---relational-data-source"></a>데이터 요금-관계형 데이터 원본 가져오기
  테이블 가져오기 마법사를 사용하여 다양한 관계형 데이터베이스에서 데이터를 가져올 수 있습니다. 마법사는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]모델 **메뉴의** 에서 사용할 수 있습니다. 데이터 원본에 연결하려면 컴퓨터에 적절한 공급자를 설치해야 합니다. 지원되는 데이터 원본 및 공급자에 대한 자세한 내용은 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)을 참조하세요.  
  
 테이블 가져오기 마법사를 사용하면 다음과 같은 데이터 원본에서 데이터를 가져올 수 있습니다.  
  
 **관계형 데이터베이스**  
  
-   Microsoft SQL Server 데이터베이스  
  
-   Microsoft SQL Azure  
  
-   Microsoft Access 데이터베이스  
  
-   Microsoft SQL Server 병렬 데이터 웨어하우스  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **다차원 원본**  
  
-   Microsoft SQL Server Analysis Services 큐브  
  
 테이블 가져오기 마법사에서는 데이터 원본이 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서인 경우 데이터를 가져올 수 없습니다.  
  
### <a name="to-import-data-from-a-database"></a>데이터베이스에서 데이터를 가져오려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **모델** 메뉴를 클릭한 다음 **데이터 원본에서 가져오기**를 클릭합니다.  
  
2.  **데이터 원본에 연결** 페이지에서 연결할 데이터베이스의 유형을 선택하고 **다음**을 클릭합니다.  
  
3.  테이블 가져오기 마법사의 단계별 지침을 따릅니다. 마법사 단계에서 **테이블 및 뷰 선택** 페이지를 사용하거나 **SQL 쿼리 지정** 페이지에서 SQL 쿼리를 만들어 특정 테이블과 뷰를 선택하거나 필터를 적용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 가져오기&#40;SSAS 테이블 형식&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
