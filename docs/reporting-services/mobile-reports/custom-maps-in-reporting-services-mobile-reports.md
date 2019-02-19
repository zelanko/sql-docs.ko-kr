---
title: Reporting Services 모바일 보고서의 사용자 지정 맵 | Microsoft Docs
description: ESRI 셰이프 파일이라는 형식으로 정의된 SQL Server 모바일 보고서 게시자의 지리적 맵에 대해 알아봅니다.
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5e34e018cbbd1ecc9dd6258111cccf7132a682e7
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289071"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Reporting Services 모바일 보고서의 사용자 지정 맵
SQL Server 모바일 보고서 게시자의 지리적 지도는 *ESRI 셰이프 파일*이라는 형식으로 정의됩니다.  
  
이 형식은 원래 비공개 기업에서 설계된 것이지만 현재는 대다수의 GIS 애플리케이션에서 널리 사용되는 반개방식 형식입니다. 이 형식에 따라 모바일 보고서 게시자에서는 지도를 정의할 때 두 개의 파일을 제공해야 합니다.  
  
- 셰이프 기하 도형용 .SHP 파일  
- 메타데이터용 .DBF 파일  
  
기본 파일 이름은 *canada.shp* 및 *canada.dbf*와 같이 일치해야 합니다. 메타데이터에는 지도에 데이터를 입력할 때 사용할 해당 셰이프의 이름(키) 값이 들어 있는 *NAME* 필드가 포함되어 있어야 합니다.  

두 지도 파일(SHP 파일 및 DBF 파일)을 합친 크기는 512KB 이하여야 합니다. 지도 파일이 너무 크면 [https://mapshaper.org/](https://mapshaper.org/) 등의 도구를 사용하여 크기를 줄입니다.  
  
[모바일 보고서에 사용자 지정 지도를 추가](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)하는 방법을 참조하세요.  
  
## <a name="technical-information"></a>기술 정보  
  
- 공식 사양: [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia 셰이프 파일 문서: [https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>지도 기하 도형 만들기 및 편집  
  
셰이프 파일을 만들고 편집하는 작업은 복잡한 프로세스이므로 이 문서에서는 설명하지 않습니다. 아래에는 이 프로세스를 시작하는 데 도움이 되는 몇 가지 리소스와 애플리케이션이 나와 있습니다.  
  
- ArcGIS: [https://www.arcgis.com/](https://www.arcgis.com/)  
- Adobe Illustrator용 MAPublisher 플러그 인: [https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS(무료): [https://www.qgis.org/](https://www.qgis.org/)  

## <a name="existing-shapefiles"></a>기존 셰이프 파일  
  
대부분의 기존 셰이프 파일은 웹의 Diva-GIS: [https://www.diva-gis.org/Data](https://www.diva-gis.org/Data)와 같은 사이트에서 다운로드할 수 있습니다.  

## <a name="see-also"></a>관련 항목:  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
