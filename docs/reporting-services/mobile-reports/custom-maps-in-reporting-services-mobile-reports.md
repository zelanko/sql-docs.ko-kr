---
title: Reporting Services 모바일 보고서의 사용자 지정 맵 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a25999826655f4ad48992ffa4705f86c9422650
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776891"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Reporting Services 모바일 보고서의 사용자 지정 맵
SQL Server 모바일 보고서 게시자의 지리적 지도는 *ESRI 셰이프 파일*이라는 형식으로 정의됩니다.  
  
이 형식은 원래 비공개 기업에서 설계된 것이지만 현재는 대다수의 GIS 응용 프로그램에서 널리 사용되는 반개방식 형식입니다. 이 형식에 따라 모바일 보고서 게시자에서는 지도를 정의할 때 두 개의 파일을 제공해야 합니다.  
  
- 셰이프 기하 도형용 .SHP 파일  
- 메타데이터용 .DBF 파일  
  
기본 파일 이름은 *canada.shp* 및 *canada.dbf*와 같이 일치해야 합니다. 메타데이터에는 지도에 데이터를 입력할 때 사용할 해당 셰이프의 이름(키) 값이 들어 있는 *NAME* 필드가 포함되어 있어야 합니다.  
  
> **참고**: 두 지도 파일(SHP 파일 및 DBF 파일)을 합친 크기는 512KB 이하여야 합니다. 지도 파일이 너무 크면 [http://mapshaper.org/](http://mapshaper.org/) 등의 도구를 사용하여 크기를 줄입니다.  
  
[모바일 보고서에 사용자 지정 지도를 추가](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)하는 방법을 참조하세요.  
  
## <a name="technical-information"></a>기술 정보  
  
- 공식 사양: [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia 셰이프 파일 문서: [http://en.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>지도 기하 도형 만들기 및 편집  
  
셰이프 파일을 만들고 편집하는 작업은 복잡한 프로세스이므로 이 문서에서는 설명하지 않습니다. 아래에는 이 프로세스를 시작하는 데 도움이 되는 몇 가지 리소스와 응용 프로그램이 나와 있습니다.  
  
- ArcGIS: [http://www.arcgis.com/](http://www.arcgis.com/)  
- Adobe Illustrator용 MAPublisher 플러그 인: [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS(무료): [http://www.qgis.org/](http://www.qgis.org/)  
- Manco ShapeFile Editor: [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>기존 셰이프 파일  
  
대부분의 기존 셰이프 파일은 웹의 다음과 같은 사이트에서 다운로드할 수 있습니다.  
  
- Diva-GIS: [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap: [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>관련 항목:  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
