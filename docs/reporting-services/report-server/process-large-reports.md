---
title: 큰 보고서 처리 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], large reports
- page breaks [Reporting Services]
- large reports
- size [SQL Server], reports
- distributing reports [Reporting Services], large reports
ms.assetid: c5275a9f-c95b-46d7-bc62-633879a8a291
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0aada8f512db681b4522dcaa24d71c1903901947
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651881"
---
# <a name="process-large-reports"></a>큰 보고서 처리
  큰 보고서는 제대로 실행될 경우 특수한 처리 문제를 발생시키며 특정 구성을 필요로 합니다. 큰 보고서는 페이지 매김을 지원하도록 구성되지 않은 한 요청 시 실행되도록 하면 안 됩니다.  
  
> [!NOTE]  
>  페이지 나누기는 기본적으로 설정되어 있습니다. 보고서에 많은 양의 데이터가 들어 있는 경우 페이지 나누기를 해제하면 안 됩니다. 처음에 보고서를 렌더링하는 데 사용된 HTML 렌더링 형식은 보고서를 브라우저에서 엽니다. 보고서의 페이지가 매겨지지 않으면 모든 데이터가 단일 페이지에 포함되므로 대부분의 브라우저에서 표시할 수 없습니다. 예를 들어 5,000행의 데이터가 포함된 보고서는 거의 대부분 브라우저에서 단일 페이지로 볼 수 없습니다.  
  
 큰 보고서로 작업할 경우 큰 문서를 수용할 수 있는 보고서 실행, 렌더링 및 배달 옵션을 선택해야 합니다. 보고서 크기는 쿼리에서 얻은 행 집합과 보고서 표시에 사용되는 렌더링 확장 프로그램에 의해 크게 좌우됩니다.  
  
 휘발성 데이터가 포함되어 있는 보고서의 경우 보고서를 실행할 때마다 크기가 급격하게 변경될 수 있습니다. 그럴 경우 데이터 원본을 모니터링하여 데이터 휘발성이 보고서에 미치는 영향 및 이 항목에 설명된 단계를 따라야 하는지 여부를 결정해야 합니다.  
  
 시간 제한 오류 및 메모리 부족 오류의 진단 방법에 대한 자세한 내용 및 팁을 보려면 blogs.msdn.com에 있는 [보고서 서버에서 보고서를 실행할 때 문제를 진단하는 방법](http://go.microsoft.com/fwlink/?LinkId=85634) 문서를 참조하세요.  
  
## <a name="configuration-recommendations"></a>구성 권장 사항  
 보고서 실행, 보고서 렌더링 및 보고서 액세스에 대한 권장 사항은 다음과 같습니다.  
  
-   페이지 매김을 지원하도록 보고서를 디자인합니다. 보고서 서버는 보고서를 한 번에 한 페이지씩 보냅니다. 보고서에 페이지 매김이 포함되어 있는 경우 브라우저에 스트림되는 데이터의 양을 제어할 수 있습니다. 자세한 내용은 [캐시 사전 로드&#40;보고서 관리자&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)를 참조하세요.  
  
-   보고서가 요청이 있을 때 실행되지 않도록 보고서를 예약된 보고서 스냅숏으로 실행되도록 구성합니다. 보고서 실행에 대한 시간 제한 값을 설정하지 마십시오. 사용률이 낮은 시간에 보고서를 실행합니다.  
  
-   보고서 처리 여부를 제어하려면 공유 데이터 원본을 사용하도록 보고서를 구성합니다. 공유 데이터 원본을 사용하면 데이터 원본 설정을 해제할 수 있다는 장점이 있습니다. 데이터 원본 설정을 해제하면 보고서가 처리되지 않습니다.  
  
-   디스크 공간을 유지하려면 보고서 기록 설정을 해제합니다. 보고서 기록 설정을 해제하려면 기록 속성 페이지의 모든 확인란을 지웁니다.  
  
-   보고서에 대한 액세스를 제한합니다. 항목 수준의 보안을 사용하도록 보고서를 구성하고 기본 역할 할당을 보고서를 필요로 하는 사용자의 액세스만 허용하는 새로운 역할 할당으로 바꿉니다.  
  
     기본적으로 사용자는 폴더 계층에서 볼 수 있는 모든 보고서를 열 수 있습니다. 보고서를 스냅숏으로 실행하도록 구성하더라도 폴더에서 보고서 항목을 볼 수 있는 사용자는 해당 보고서를 열 수 있습니다. 보고서가 아주 클 경우 사용자가 보고서 관리자에서 보고서를 열 때 브라우저가 응답하지 않을 수 있습니다.  
  
## <a name="rendering-recommendations"></a>렌더링 권장 사항  
 보고서 배포를 구성하기 전에 큰 문서를 수용할 수 있는 렌더링 클라이언트를 알고 있어야 합니다. 권장되는 형식은 소프트 페이지 나누기가 적용된 기본 HTML 렌더링 확장 프로그램이지만 페이지 매김을 지원하는 다른 형식을 선택할 수도 있습니다.  
  
 성능과 메모리 사용량은 렌더링 형식에 따라 다릅니다. 같은 보고서라도 선택하는 형식에 따라 렌더링 속도와 필요한 메모리 양이 다릅니다. 가장 빠르고 메모리를 적게 사용하는 형식은 CSV, XML 및 HTML입니다. PDF와 Excel은 각각 다른 이유로 성능이 가장 낮습니다. PDF는 CPU를 많이 사용하고 Excel은 RAM을 많이 사용합니다. 이미지 렌더링은 이러한 두 그룹 사이에 있습니다. 보고서 배포 방법을 정의할 때 형식을 지정할 수 있습니다.  
  
## <a name="deployment-and-distribution-recommendations"></a>배포 권장 사항  
 페이지 나누기를 사용하여 보고서 렌더링을 제어할 경우 일반 보고서를 배포할 때와 동일한 방식으로 큰 보고서를 배포할 수 있습니다. 보고서 관리자, SharePoint 웹 파트 또는 포털이나 웹 사이트에 추가한 URL을 통해 보고서에 액세스하도록 할 수 있습니다. 이러한 모든 배포 옵션은 이전에 실행된 보고서 스냅숏뿐만 아니라 요청 시 액세스를 지원합니다.  
  
 이러한 방법 대신 개인 사용자에게 보고서를 배포할 수도 있습니다. 배달 옵션을 주의해서 구성하면 구독을 통해 큰 보고서를 배포할 수 있습니다. 표준 구독 또는 데이터 기반 구독을 사용하여 보고서를 배달할 수 있습니다. 구독 및 배달 권장 사항은 다음과 같습니다.  
  
-   웹 보관 파일(MHTML), PDF 또는 Excel을 사용하도록 구독을 구성합니다.  
  
-   PDF 또는 Excel을 사용할 경우 파일 공유 배달을 사용하도록 구독을 구성합니다. 배달된 보고서는 데스크톱 응용 프로그램을 통해 사용할 수 있습니다. 파일 공유에 대한 사용 권한을 설정하여 보고서를 볼 수 있는 사용자를 결정해야 합니다.  
  
     보고서가 파일 공유에 저장되면 해당 보고서는 더 이상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 의해 제어되거나 보안되지 않습니다. 보고서가 업데이트될 때 알림을 받으려면 전자 메일 배달을 사용하여 알림만 보내는 두 번째 구독을 만듭니다.  
  
 전자 메일 보고서 배달을 사용하려면 링크를 포함하도록 구독을 구성합니다. 보고서를 첨부 파일로 보내지는 마십시오.  
  
## <a name="see-also"></a>참고 항목  
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [캐시 사전 로드&#40;보고서 관리자&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  
