---
title: 보고서 및 스냅숏 크기 제한 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- large reports
- maximum report size
- size [SQL Server], reports
- report size [Reporting Services]
- reports [Reporting Services], size
- denial of service attacks [Reporting Services]
ms.assetid: 1e3be259-d453-4802-b2f5-6b81ef607edf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 964c6dace976f54e053947c301b3093de5aa921f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217953"
---
# <a name="report-and-snapshot-size-limits"></a>보고서 및 스냅숏 크기 제한
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포를 관리하는 관리자는 이 항목의 정보를 통해 보고서가 보고서 서버에 게시되고, 런타임에 렌더링되고, 파일 시스템에 저장될 때 적용되는 보고서 크기 제한을 이해할 수 있습니다. 이 항목에서는 보고서 서버 데이터베이스의 크기를 측정하는 방법에 대한 지침을 제공하고 스냅숏 크기가 서버 성능에 미치는 영향에 대해 설명합니다.  
  
## <a name="maximum-size-for-published-reports-and-models"></a>게시된 보고서 및 모델의 최대 크기  
 보고서 서버에서 보고서 및 모델 크기는 보고서 서버에 게시하는 보고서 정의 파일(.rdl) 및 보고서 모델 파일(.smdl)의 크기를 기반으로 합니다. 보고서 서버에서는 사용자가 게시하는 보고서나 모델의 크기를 제한하지 않습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서는 서버에 게시되는 항목에 대한 최대 크기를 제한합니다. 기본적으로 이 제한은 4MB입니다. 이 제한을 초과하는 파일을 보고서 서버에 업로드하거나 게시하면 HTTP 예외가 발생합니다. 이런 경우 Machine.config 파일에서 `maxRequestLength` 요소의 값을 늘려 기본값을 수정할 수 있습니다.  
  
 보고서 모델은 매우 클 수 있지만 보고서 정의는 대부분 4MB를 초과하지 않습니다. 일반적인 보고서 크기는 KB 단위입니다. 그러나 포함 이미지를 포함시키면 해당 이미지에 대한 인코딩으로 인해 보고서 정의가 4MB의 기본값을 초과할 수 있습니다.  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서는 게시되는 파일에 대한 최대 제한을 적용하여 서버에 대한 서비스 거부 공격 위협을 줄입니다. 상한값을 늘리면 이 제한에 따른 보호 기능이 손상됩니다. 따라서 추가 보안 위험을 능가하는 이점이 있다는 확신이 있는 경우에만 이 값을 늘리십시오.  
  
 `maxRequestLength` 요소에 대해 설정하는 값은 적용하려는 실제 크기 제한보다 커야 합니다. 모든 매개 변수가 SOAP Envelope에 캡슐화되고 Base64 인코딩이 <xref:ReportService2010.ReportingService2010.CreateReportEditSession%2A> 및 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> 메서드의 Definition 매개 변수와 같은 특정 매개 변수에 적용된 후 발생하는 HTTP 요청 크기의 불가피한 증가를 수용하기 위해 더 큰 값을 설정해야 합니다. Base64 인코딩은 원래 데이터의 크기를 33% 정도 증가시킵니다. 결과적으로 지정 하는 값에 대 한는 `maxRequestLength` 요소에서 실제로 사용 가능한 항목 크기 보다 33% 정도 해야 합니다. 예를 들어 `maxRequestLength`의 값으로 64MB를 지정하는 경우, 실제로 보고서 서버에 게시되는 보고서 파일의 최대 크기를 48MB 정도로 예상할 수 있습니다.  
  
## <a name="report-size-in-memory"></a>메모리의 보고서 크기  
 보고서를 실행하면 보고서 크기는 출력 스트림 크기와 보고서에 반환된 데이터 양을 더한 크기가 됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 렌더링되는 보고서의 크기에 대한 최대 제한을 적용하지 않습니다. 최대 크기 제한은 시스템 메모리에 따라 결정됩니다. 기본적으로 보고서 서버에서는 보고서를 렌더링할 때 사용 가능한 구성 메모리를 모두 사용하지만 구성 설정을 지정하여 메모리 임계값과 메모리 관리 정책을 지정할 수 있습니다. 자세한 내용은 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)을 참조하세요.  
  
 모든 보고서의 크기는 반환되는 데이터 양과 보고서에 사용된 렌더링 형식에 따라 크게 달라질 수 있습니다. 매개 변수가 있는 보고서의 크기는 매개 변수 값이 쿼리 결과에 미치는 영향에 따라 커지거나 작아질 수 있습니다. 선택한 보고서 출력 형식은 다음과 같은 방식으로 보고서 크기에 영향을 줍니다.  
  
-   HTML은 보고서를 한 번에 한 페이지씩 처리합니다. 보고서는 작은 단위로 처리되므로 특정 청크를 처리하는 데 많은 양의 메모리가 필요하지 않습니다.  
  
-   PDF, Excel, TIFF, XML 및 CSV는 메모리에 있는 전체 보고서를 처리한 다음 해당 보고서를 사용자에게 표시합니다.  
  
 렌더링된 보고서의 크기를 측정하려면 보고서 실행 로그를 확인합니다. 자세한 내용은 [보고서 서버 실행 로그 및 ExecutionLog3 뷰](report-server-executionlog-and-the-executionlog3-view.md)합니다.  
  
 디스크에 있는 렌더링된 보고서의 크기를 계산하려면 보고서를 파일 시스템으로 내보내고 저장합니다. 저장된 파일에 데이터 및 보고서 형식 정보가 들어 있습니다.  
  
 Excel 형식으로 렌더링할 때만 보고서 크기가 엄격하게 제한됩니다. 워크시트의 행과 열은 각각 65536개와 256개를 초과할 수 없습니다. 다른 렌더링 형식은 이러한 제한이 없으므로 서버에 있는 리소스 양에 의해서만 크기가 제한됩니다. Excel 파일 제한에 대 한 자세한 내용은 참조 하세요. [다른 파일 형식으로 보고서 내보내기 &#40;보고서 작성기 및 SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  보고서 처리 및 렌더링은 메모리에서 수행됩니다. 보고서가 크거나 사용자 수가 많은 경우에는 보고서 서버 배포가 사용자에게 만족스러운 수준에서 수행될 수 있도록 용량 계획을 세워야 합니다. 도구 및 지침에 대한 자세한 내용은 MSDN의 [Reporting Services의 확장성 및 성능 계획](http://go.microsoft.com/fwlink/?LinkID=70650) 및 [Visual Studio 2005를 사용한 SQL Server 2005 Reporting Services 보고서 서버의 부하 테스트 수행](http://go.microsoft.com/fwlink/?LinkID=77519)을 참조하십시오.  
  
## <a name="measuring-snapshot-storage"></a>스냅숏 저장소 측정  
 특정 스냅숏의 크기는 보고서에 있는 데이터 양에 비례합니다. 스냅숏은 일반적으로 보고서 서버에 저장된 다른 항목보다 훨씬 큽니다. 스냅숏 크기는 몇 MB에서 수십 MB에 이르기까지 다양합니다. 보고서가 아주 큰 경우 스냅숏은 훨씬 더 커집니다. 스냅숏 사용 빈도와 보고서 기록 구성 방법에 따라 보고서 서버 데이터베이스에 필요한 디스크 공간 크기가 짧은 기간 동안에 빠르게 늘어날 수 있습니다.  
  
 기본적으로 **reportserver** 및 **reportservertempdb** 데이터베이스는 모두 자동 증가로 설정되어 있습니다. 데이터베이스 크기는 자동으로 늘어날 수는 있지만 자동으로 줄어들지는 않습니다. 스냅숏을 삭제했기 때문에 **reportserver** 데이터베이스 크기가 너무 큰 경우에는 이 데이터베이스 크기를 직접 줄여서 디스크 공간을 복구해야 합니다. 마찬가지로 **reportservertempdb** 가 크기가 아주 큰 대화형 보고 기능을 사용할 수 있을 만큼 커진 경우에는 사용자가 크기를 줄일 때까지 이 설정으로 디스크 공간 할당이 유지됩니다.  
  
 보고서 서버 데이터베이스의 크기를 측정하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행합니다. 정기적으로 총 데이터베이스 크기를 계산하면 시간에 따른 보고서 서버 데이터베이스의 공간 할당량을 적절히 예측하는 데 도움이 됩니다. 다음 문은 현재 사용하고 있는 공간을 측정합니다. 이 문에서는 사용자가 기본 데이터베이스 이름을 사용하고 있다고 가정합니다.  
  
```  
USE ReportServer  
EXEC sp_spaceused  
```  
  
## <a name="snapshot-size-and-report-server-performance"></a>스냅숏 크기 및 보고서 서버 성능  
 스냅숏 크기는 보고서가 처리되고 렌더링될 때 서버 성능에 영향을 줍니다. 서버 성능은 대부분 렌더링 작업의 영향을 받으므로 스냅숏이 큰 경우에는 사용자가 보고서를 요청할 때 지연이 발생할 수 있습니다. 사용자 수에 따라 스냅숏 크기가 100MB 이상이면 지연이 발생할 수 있습니다.  
  
 큰 스냅숏으로 인한 성능 지연을 최소화하려면 다음을 수행합니다.  
  
-   보고서 서버와 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 을 별도의 컴퓨터에 배포합니다.  
  
-   시스템 메모리를 더 많이 추가합니다.  
  
-   회사의 보고서 서버를 구성하는 방법에 대한 유용한 정보를 보려면 MSDN 웹 사이트에서 "Reporting Services의 확장성 및 성능 계획(Planning for Scalability and Performance with Reporting Services)" 문서를 검토하십시오.  
  
 보고서 서버 데이터베이스에 저장되어 있는 스냅숏의 수량 자체는 성능에 영향을 주지 않습니다. 서버 성능에 영향을 주지 않고 수많은 스냅숏을 저장할 수 있습니다. 스냅숏은 무제한으로 보관할 수 있습니다. 그러나 보고서 기록은 구성할 수 있습니다. 보고서 서버 관리자가 보고서 기록 제한을 낮추면 보관하려고 한 기록 보고서가 손실될 수 있습니다. 보고서를 삭제하면 모든 보고서 기록도 함께 삭제됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 처리 속성 설정](set-report-processing-properties.md)   
 [보고서 서버 데이터베이스를 &#40;SSRS 기본 모드&#41;](report-server-database-ssrs-native-mode.md)   
 [큰 보고서 처리](process-large-reports.md)  
  
  
