---
title: "Master Data Services로 Data Quality Services 통합 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 50488f539ba00055f4b515a41dca47594c5d3f0d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>MDS(Master Data Services)와 Data Quality Services의 통합 설정
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 일치 기능은 DQS(Data Quality Services)에서 제공됩니다. 이 기능은 먼저 설정해야 사용할 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 응용 프로그램 및 데이터베이스가 있어야 합니다.  
  
-   Data Quality Services 기능과 데이터 품질 클라이언트는 MDS 데이터베이스를 호스팅하는 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치해야 합니다. 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)을 참조하세요.  
  
### <a name="to-enable-data-quality-services-integration"></a>Data Quality Services 통합을 사용하려면  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
2.  왼쪽 창에서 **웹 구성**을 클릭합니다.  
  
3.  **웹 구성** 페이지에서 웹 사이트 및 웹 응용 프로그램을 선택합니다.  
  
4.  **DQS 통합 사용** 섹션에서 **Data Quality Services와 통합 사용**을 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Excel용 MDS 추가 기능의 데이터 품질 일치](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Microsoft Excel용 Master Data Services 추가 기능](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
