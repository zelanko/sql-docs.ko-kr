---
title: "XML 편집기(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.editor.xml.f1
- sql13.swb.editorxml.f1
- vs.xmleditor
- sql13.swb.xmleditor.f1
helpviewer_keywords: XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bc3cfd22e1bff42f4ea4730337d01da0c2d5f6a7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="xml-editor-sql-server-management-studio"></a>XML 편집기(SQL Server Management Studio)
  XML 스키마, ADO.NET 데이터 집합 및 XML 문서 작업에 사용할 수 있는 다양한 시각적 도구를 제공합니다. XML 디자이너는 WC3(World Wide Web Consortium)에서 정의한 XSD(XML 스키마 정의) 언어를 지원합니다. DTD(문서 유형 정의)나 XDR(XML-Data Reduced)와 같은 다른 XML 스키마 언어는 지원하지 않습니다.  
  
 디자이너를 표시하려면 데이터 집합, XML 스키마 또는 XML 파일을 프로젝트에 추가하거나 아래 표에 나오는 파일 형식을 여십시오.  
  
> [!CAUTION]  
>  스키마 뷰에서 작업할 때는 **실행 취소** 명령을 사용할 수 없으므로 작업을 신중하게 계획하고 파일을 자주 저장하는 것이 좋습니다.  
  
 XML 디자이너는 XML 파일, XML 스키마 및 데이터 집합 작업에 다음 세 가지 뷰(또는 모드)를 제공합니다.  
  
|보기|설명|지원되는 파일 형식|  
|----------|-----------------|--------------------------|  
|**스키마**|XML 스키마 및 ADO.NET 데이터 집합을 시각적으로 만들고 수정할 때 사용|.xsd|  
|**데이터**|구조화된 데이터 표에서 XML 데이터 파일을 시각적으로 수정할 때 사용|.xml|  
|**XML**|XML을 편집할 때 사용. 원본 편집기는 색 구분과 단어 자동 완성 및 멤버 목록 표시를 비롯한 IntelliSense 기능 제공|.xml .xsd .xslt .wsdl .web. resx .tdl. wsf .hta .disco .vsdisco .config|  
|**실행 계획**|SET SHOWPLAN_XML ON 옵션을 사용하여 만든 xml 쿼리 계획 표시|.showplan|  
  
## <a name="schema-view"></a>스키마 뷰  
 스키마 뷰는 XML 스키마와 ADO.NET 데이터 집합을 구성하는 요소, 특성, 유형 등을 시각적으로 보여 줍니다.  
  
 스키마 뷰에서는 도구 상자의 XML 스키마 탭이나 서버 탐색기 중 하나에서 디자인 화면으로 요소를 끌어 놓아 스키마와 데이터 집합을 만들 수 있습니다. 또한 디자인 화면을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 추가를 선택하여 요소를 디자이너에 추가할 수도 있습니다.  
  
 스키마 뷰에서는 다음 작업을 수행할 수 있습니다.  
  
-   기존 XML 스키마와 ADO.NET 데이터 집합 생성 및 수정  
  
-   테이블 간 관계 만들기 및 편집  
  
-   키 만들기 및 편집  
  
-   XML 스키마에서 ADO.NET 데이터 집합 생성  
  
> [!NOTE]  
>  스키마 뷰에서 요소의 레이아웃은 .xsx 파일로 저장됩니다. 솔루션 탐색기 도구 모음에서 **모든 파일 표시** 를 클릭한 다음 .xsd 파일을 확장하면 이 파일을 볼 수 있습니다. .xsx 파일이 표시되지 않으면 이전에 XML 디자이너에서 .xsd 파일을 열어본 적이 없는 것입니다.  
  
### <a name="customizing-schema-view"></a>스키마 뷰 사용자 지정  
 다음 기능은 스키마 뷰에서 요소의 시각적 레이아웃을 수정하는 데 사용됩니다.  
  
-   확대/축소  
  
-   중첩된 요소 확장 또는 축소  
  
-   요소 레이아웃 자동 정렬  
  
-   축소된 요소의 기본 상태 다시 설정  
  
##### <a name="to-expand-hidden-nested-elements"></a>숨겨진 중첩 요소를 확장하려면  
  
-   요소 아래쪽의 더하기 아이콘을 클릭합니다.  
  
##### <a name="to-collapse-nested-elements"></a>중첩 요소를 축소하려면  
  
-   디자이너에 표시하려는 맨 아래 요소의 빼기 아이콘을 클릭합니다.  
  
## <a name="data-view"></a>데이터 뷰  
 데이터 뷰는 .xml 파일을 수정하는 데 사용할 수 있는 데이터 표를 제공합니다. 데이터 뷰에서는 XML 파일의 내용만 편집할 수 있으며 태그와 구조는 편집할 수 없습니다.  
  
 데이터 뷰에는 **데이터 테이블** 및 **데이터**의 두 가지 별도 영역이 있습니다. **데이터 테이블** 영역은 XML 파일에 정의되어 있는 관계를 중첩된 순서(바깥쪽에서부터 안쪽으로)대로 보여 주는 목록입니다. **데이터** 영역은 데이터 테이블 영역에서 선택한 내용에 따라 해당 데이터를 표시하는 데이터 표입니다.  
  
> [!NOTE]  
>  새로 만든 XML 파일에는 데이터가 들어 있지 않으므로 데이터 뷰에서 표시할 수 없습니다. 이외에도 일부 XML 문서에서는 데이터 뷰를 실행할 수 없습니다. XML의 형식이 올바르더라도 구조화된 데이터가 아닌 경우 데이터 뷰로 전환하려고 하면 "이 XML 문서는 형식이 올바르지만 데이터 뷰에서 표시할 수 없는 구조를 포함하고 있습니다"라는 메시지가 표시됩니다.  
  
 데이터 뷰에서는 다음 작업을 수행할 수 있습니다.  
  
-   수동으로 데이터 테이블 채우기  
  
-   기존 데이터 테이블 편집  
  
-   XML 문서에서 XML 스키마 생성  
  
## <a name="xml-view"></a>XML 뷰  
 XML 뷰는 원시 XML을 편집할 수 있는 편집기와 IntelliSense 및 색 구분 기능을 제공합니다. 스키마가 연결되어 있는 .xml 파일과 .xsd 파일로 작업할 때는 문 완성 기능을 사용할 수 있습니다. 태그를 시작하는 <를 입력하면 해당 위치에 들어갈 수 있는 요소가 목록으로 표시됩니다. 요소 이름을 입력한 후 스페이스바를 누르면 요소가 지원하는 특성이 목록으로 표시됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 옵션은 도구 모음에서 사용할 수 없습니다. XML 편집기에서 이 옵션을 사용하려면 **편집** 메뉴에서 **IntelliSense**를 클릭합니다.  
  
## <a name="showplan-view"></a>실행 계획 뷰  
 SET SHOWPLAN_XML ON 옵션을 사용하여 만든 쿼리 계획을 XML 형식으로 저장할 수 있습니다. 쿼리 계획을 열려면 확장명이 .showplan인 파일을 두 번 클릭하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 실행 계획 저장](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
