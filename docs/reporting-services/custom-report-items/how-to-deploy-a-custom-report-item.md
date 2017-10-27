---
title: "방법: 사용자 지정 보고서 항목 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: 26
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 742e80b96e6887188620b4f2a7ab3808475ceda2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="how-to-deploy-a-custom-report-item"></a>방법: 사용자 지정 보고서 항목 배포
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용자 지정 보고서 항목을 배포하려면 보고서 서버 구성 파일을 수정하고 디자인 타임 및 런타임 구성 요소 어셈블리를 보고서 디자이너와 보고서 서버 양쪽의 적절한 응용 프로그램 폴더로 복사해야 합니다.  
  
### <a name="to-deploy-a-custom-report-item"></a>사용자 지정 보고서 항목을 배포하려면  
  
1.  Rsreportdesigner.config 파일을 편집하여 디자이너에서 사용하도록 사용자 지정 보고서 항목 런타임 및 디자인 타임 구성 요소를 구성합니다. **ReportItemName** 엔트리 일치 해야 합니다는 **CustomReportItemAttribute** 에 사용 된 특성 프로그램 **CustomReportItemDesigner** 클래스입니다. 예를 들어  
  
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
  
2.  Rsreportserver.config 파일을 편집하여 사용자 지정 보고서 항목 런타임 구성 요소를 등록합니다. 예를 들어  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Rsssrvpolicy.config 파일을 편집 추가 **CodeGroup** 사용자 지정 보고서 항목에 적합 한 권한을 부여 하는 합니다. 예를 들어  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [사용자 지정 보고서 항목 클래스 라이브러리](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  

