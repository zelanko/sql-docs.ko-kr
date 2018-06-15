---
title: Reporting Services 모바일 보고서에 대한 Excel 데이터 준비 | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 76f71b0f284602ae1860fcba5bc69f9221b0be33
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019604"
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Reporting Services 모바일 보고서에 대한 Excel 데이터 준비
  
다음은 Excel 파일 및 통합 문서를 모바일 보고서에 사용하도록 준비할 때 염두에 두어야 할 몇 가지 사항입니다.  
  
## <a name="do"></a>해야 할 일  
  
- 데이터 집합당 통합 문서 한 개를 지정합니다.  
- 첫 번째 행에 열 머리글을 지정합니다.  
- 각 열 내에서 데이터 형식을 일관성 있게 유지합니다.  
- Excel에서 셀을 적절한 형식으로 지정합니다.  
- Excel에서 데이터를 데이터 모델이 아닌 워크시트에 지정합니다.  
- 수식을 사용할 때 전체 열이 같은 수식을 사용하여 계산되도록 합니다.  
- Excel 2007 이상을 사용합니다.  
- Excel 파일을 확장명 XLSX로 저장합니다.  
          
## <a name="dont"></a>하지 않아야 할 일  
  
- 이미지, 그래프, 피벗 테이블 또는 기타 포함된 개체를 데이터 집합 워크시트에 포함합니다.  
- 총 또는 계산된 행을 포함합니다.  
- 가져올 때 파일을 Excel에서 열린 상태로 유지합니다.  
- 통화 또는 다른 기호를 추가하여 숫자를 수동으로 서식 지정합니다.  
- 데이터가 데이터 모델에 저장된 통합 문서를 사용합니다.  
  
## <a name="worksheets"></a>워크시트  
          
Excel 파일을 모바일 보고서에 대한 데이터 집합으로 준비할 때에는 데이터 집합이 워크시트당 한 개만 있도록 합니다. 각 개별 워크시트를 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 에 별도 테이블로 가져옵니다. 여러 Excel 원본에서 나온 동일한 이름의 워크시트는 가져올 때 증가하는 번호를 추가하여 이름이 변경됩니다. 예를 들어 통합 문서에 "MyWorksheet"라는 워크시트 3개가 있는 경우 두 번째 및 세 번째 워크시트는 "MyWorksheet0" 및 "MyWorksheet1"로 이름 변경됩니다. 다음 스크린샷은 가져오도록 준비된 최적의 Excel 워크시트의 처음 몇 행을 보여 줍니다.  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>열 머리글  
  
위의 예제에서 볼 수 있듯이 첫 번째 행은 해당 열의 메트릭 이름을 포함하고 있습니다. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 은 갤러리 요소에서 쉽게 참조하도록 이러한 열 머리글을 유지합니다. 하지만 열 머리글은 필요 없습니다. 누락된 경우 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 은 Excel A,B,C,...,AA,BB,... 규칙을 사용하여 머리글을 생성합니다.  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]은 Excel 통합 문서를 가져올 때 각 열의 처음 두 셀의 데이터 형식을 비교하여 첫 번째 행 머리글을 자동으로 검색합니다. 어떤 열의 처음 두 셀의 데이터 형식이 일치하지 않으면 첫 번째 행이 열 머리글을 포함하도록 결정됩니다. 따라서 테이블에 숫자 열 머리글이 있는 경우 가져오기 프로세스에서 머리글로 검색되도록 머리글 이름에 문자열 접두사를 추가합니다.  
  
## <a name="cells"></a>셀  
  
워크시트 데이터 집합의 각 열에 있는 셀 데이터는 일관성이 있어야 합니다. 각 열에는 가져올 때 데이터 형식이 할당됩니다. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 은 자동으로 데이터 형식을 문자열, double(숫자), 부울(true/false) 또는 날짜/시간으로 검색합니다. 같은 열에 데이터 형식이 섞여 있으면 이 검색이 부정확하거나 완전히 실패할 수 있습니다. 이 검색에서는 문자열 형식인 예상 열 머리글을 고려합니다. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 이 원하는 형식을 검색하도록 Excel에서 셀을 정확한 형식으로 서식 지정해야 합니다. 위의 예제에서 열 6개는 다음 형식으로 지정될 수 있습니다.  
*  datetime 열  
*  문자열 열  
*  double 열  
  
워크시트에 계산된 셀 또는 수식이 포함된 경우 결과 표시 값만을 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]으로 가져옵니다.  
  
## <a name="file-location-and-refreshing-excel-data"></a>파일의 위치 및 Excel 데이터 새로 고침  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]에 가져오는 Excel 파일을 저장하는 위치에 관한 제한은 없습니다. 그러나 파일을 가져온 후 이동하거나 이름 변경하는 경우 데이터 뷰에서 찾을 수 있는 **모든 데이터 새로 고침** 명령을 통해 해당 데이터를 새로 고칠 수 없습니다.   
  
>**참고**: [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 은 Excel 데이터를 새로 고치지 않습니다. 이동하지 않은 경우에만 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **새로 고침** 명령을 통해 데이터를 새로 고칠 수 있습니다.  
  
## <a name="dates"></a>날짜  
  
날짜 필드는 많은 모바일 보고서에 필수이므로 셀을 Excel의 날짜로 올바르게 서식 지정합니다. 일부 경우에는 이 때문에 변환이 필요합니다. 다음은 셀을 텍스트에서 Excel의 날짜로 변환하는 수식의 예입니다.  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
셀을 변환한 후 셀 또는 **범주** 목록에서 전체 열 > **컨텍스트** 메뉴 > **셀 서식** > **날짜**를 선택하여 날짜로 서식 지정해야 합니다. 또한 Excel의 텍스트 열 변환 마법사를 사용하여 텍스트 셀을 올바르게 서식 지정된 날짜로 변환할 수 있습니다.  
  
## <a name="unsupported"></a>지원되지 않음  
  
위에서 설명한 것과 다른 형식의 워크시트 데이터는 가져올 때 예기치 않은 결과를 야기할 수 있습니다. Excel 파일의 워크시트를 모바일 보고서와 함께 사용하기 위해 올바른 형식의 워크시트로 제한하는 것이 좋습니다.  
  
피벗 테이블, 시각화 및 이미지를 포함한 Excel 워크시트의 사용자 지정 개체는 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]에 가져오지 않습니다.  
  
### <a name="see-also"></a>관련 항목:  
- [Prepare data for Reporting Services mobile reports](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  보기(iOS용 Power BI)  
-  [iPhone 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) 보기(iOS용 Power BI)  
  
  
  
  
  
  
  

