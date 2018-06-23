---
title: '방법: 사용자 지정 보고서 항목 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: 25
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c65d3a2f3fd26fd87c8471676d68a052126c542c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173277"
---
# <a name="how-to-deploy-a-custom-report-item"></a>방법: 사용자 지정 보고서 항목 배포
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용자 지정 보고서 항목을 배포하려면 보고서 서버 구성 파일을 수정하고 디자인 타임 및 런타임 구성 요소 어셈블리를 보고서 디자이너와 보고서 서버 양쪽의 적절한 응용 프로그램 폴더로 복사해야 합니다.  
  
### <a name="to-deploy-a-custom-report-item"></a>사용자 지정 보고서 항목을 배포하려면  
  
1.  Rsreportdesigner.config 파일을 편집하여 디자이너에서 사용하도록 사용자 지정 보고서 항목 런타임 및 디자인 타임 구성 요소를 구성합니다. `ReportItemName` 항목이 `CustomReportItemAttribute` 클래스에 사용되는 `CustomReportItemDesigner` 특성과 일치해야 합니다. 예를 들어:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  Rsreportserver.config 파일을 편집하여 사용자 지정 보고서 항목 런타임 구성 요소를 등록합니다. 예를 들어:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Rsssrvpolicy.config 파일을 편집하여 사용자 지정 보고서 항목에 적절한 권한을 부여하는 `CodeGroup`을 추가합니다. 예를 들어:  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  사용자 지정 보고서 항목 런타임 구성 요소 DLL을 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 및 \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin 디렉터리로 복사합니다.  
  
5.  사용자 지정 보고서 항목 디자인 타임 구성 요소 DLL을 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 디렉터리로 복사합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 파일](../report-server/reporting-services-configuration-files.md)   
 [사용자 지정 보고서 항목 클래스 라이브러리](custom-report-item-class-libraries.md)  
  
  