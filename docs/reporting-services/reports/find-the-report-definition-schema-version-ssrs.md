---
title: 보고서 정의 스키마 버전 찾기(SSRS) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 129fcb8e1533162560b88e9400c68c7c863be119
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826836"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>보고서 정의 스키마 버전 찾기(SSRS)

보고서 정의 파일은 rdl 파일의 유효성을 검사하는 데 사용되는 보고서 정의 스키마의 버전에 대한 RDL 네임스페이스를 지정합니다. 보고서 제작 환경 등의 보고서 디자이너에서에서.rdl 파일을 열면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], Visual Studio 또는 보고서 작성기. 이전 네임 스페이스용으로 만든 보고서를 백업 파일을 자동으로 만들어진 하 고 보고서가 현재 네임 스페이스로 업그레이드 됩니다. 업그레이드된 보고서 정의를 저장하면 변환된 .rdl 파일이 저장됩니다. 이 방법은 보고서 정의를 업그레이드할 수 있는 유일한 방법입니다. 보고서 정의 자체는 보고서 서버에서 업그레이드되지 않습니다. 컴파일된 보고서는 보고서 서버에서 업그레이드됩니다. 자세한 내용은 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)을(를) 참조하세요.  
  
## <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>방법: 보고서의 RDL 스키마 버전 확인  
  
1. XML을 볼 수 있는 메모장이나 XML 메모장과 같은 애플리케이션에서 보고서 .rdl 파일을 엽니다.  
  
     XML 보고서 요소는 스키마 네임스페이스를 지정합니다. 예를 들어 다음 보고서 요소는 보고서 디자이너에 대한 네임스페이스와 보고서 정의에 대한 네임스페이스를 지정합니다.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     최신 보고서 정의 네임 스페이스는 2016입니다. 그러나 최근 게시 된 보고서 정의 네임 스페이스는 2010 이며, 다음 url 지정: `https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`...
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>방법: 보고서 디자이너의 RDL 스키마 버전 확인  
  
1.  새 프로젝트를 엽니다. 선택한 프로젝트의 버전에 따라 RDL 스키마 버전이 결정됩니다. SQL Server에서는 둘 이상의 스키마 버전이 지원됩니다. 자세한 내용은 [SQL Server Data Tools의 배포 및 버전 지원](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)을 참조하세요.  
  
2.  **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **템플릿** 창에서 **보고서**를 클릭합니다.  
  
4.  **이름**에 보고서 이름을 입력하거나 기본 이름을 적용합니다.  
  
5.  **추가**를 클릭합니다. 보고서 디자이너의 디자인 뷰에 새 보고서가 열립니다.  
  
6.  **보기** 메뉴에서 **코드**를 클릭합니다. 보고서 정의가 XML 파일로 표시됩니다.  
  
    XML 보고서 요소는 스키마 네임스페이스를 지정합니다. 예를 들어 다음 보고서 요소는 보고서 디자이너에 대한 네임스페이스와 보고서 정의에 대한 네임스페이스를 지정합니다.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     보고서 정의 네임스페이스는 다음 URL `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>방법: 보고서 서버의 RDL 스키마 버전 확인  
  
-   웹 포털에서 보고서 서버에 대 한 URL을 입력 합니다. 예를 들어 다음 URL은 로컬 컴퓨터의 보고서 서버를 지정합니다.  
  
     `https://localhost/reportserver/reportdefinition.xsd`  
  
     .xsd 파일이 브라우저에서 열립니다.  
  
     XML 스키마 요소는 스키마 네임스페이스를 지정합니다. 예를 들어 다음 스키마 요소는 3개의 네임스페이스, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 내부적으로 사용되는 targetNamespace 참조, 스키마 자체에 대한 xsd 참조(xsd) 및 보고서 정의 참조를 지정합니다.  *연도* 보고서를 사용 하 여 스키마의 연도 나타냅니다. 예를 들어, 2010 또는 2016
  
    ``` XML  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" elementFormDefault="qualified">  
    ```  
  
     보고서 정의 네임스페이스는 다음 URL `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  

## <a name="next-steps"></a>다음 단계
[보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)   
[RDL(Report Definition Language)](../../reporting-services/reports/report-definition-language-ssrs.md)   

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
