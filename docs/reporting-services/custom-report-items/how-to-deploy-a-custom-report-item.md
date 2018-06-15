---
title: '방법: 사용자 지정 보고서 항목 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: custom-report-items
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: 26
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2d4bebf1490bb2da15486fce177932cb1aecf5c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014380"
---
# <a name="how-to-deploy-a-custom-report-item"></a>방법: 사용자 지정 보고서 항목 배포
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용자 지정 보고서 항목을 배포하려면 보고서 서버 구성 파일을 수정하고 디자인 타임 및 런타임 구성 요소 어셈블리를 보고서 디자이너와 보고서 서버 양쪽의 적절한 응용 프로그램 폴더로 복사해야 합니다.  
  
### <a name="to-deploy-a-custom-report-item"></a>사용자 지정 보고서 항목을 배포하려면  
  
1.  Rsreportdesigner.config 파일을 편집하여 디자이너에서 사용하도록 사용자 지정 보고서 항목 런타임 및 디자인 타임 구성 요소를 구성합니다. **ReportItemName** 항목은 **CustomReportItemDesigner** 클래스의 **CustomReportItemAttribute** 특성과 일치해야 합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
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
  
2.  Rsreportserver.config 파일을 편집하여 사용자 지정 보고서 항목 런타임 구성 요소를 등록합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Rsssrvpolicy.config 파일을 편집하여 사용자 지정 보고서 항목에 적절한 권한을 부여하는 **CodeGroup**을 추가합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
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
  
  
