---
title: 연결(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a7d336e777f4f6bf00310cbadfed75987ba45252
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478945"
---
# <a name="connections-mds-add-in-for-excel"></a>연결(Excel용 MDS 추가 기능)
  데이터를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에 다운로드하려면 먼저 연결을 만들어야 합니다. 연결은 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 서비스가 연결할 MDS 데이터베이스를 확인하는 방법입니다.  
  
 연결 문자열은 일반적으로 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 URL입니다(예: http://contoso/mds ).  
  
 Excel을 시작할 때마다 MDS 저장소에 연결해야 합니다. 이에 대한 유일한 예외는 활성 스프레드시트에 이미 MDS 관리 데이터가 포함된 경우입니다. 이 경우 사용자가 새로 고치거나 시트의 데이터를 게시할 때마다 연결이 자동으로 수행됩니다.  
  
 여러 연결을 만들 수 있습니다. 가장 최근에 액세스한 연결은 기본값으로 간주됩니다.  
  
 여러 사용자가 동시에 연결할 수 있습니다. 하지만 여러 사용자가 동일한 데이터를 게시하려고 시도하면 충돌이 발생할 수 있습니다. 자세한 내용은 [데이터 게시 &#40;MDS 추가 기능에 Excel에 대 한&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)합니다.  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>자동으로 연결 및 자주 사용되는 데이터 로드  
 항상 동일한 서버에 연결하고 동일한 데이터 집합을 로드하려는 경우 연결 및 필터 정보를 포함하는 바로 가기 쿼리 파일을 만들 수 있습니다. 쿼리 파일에 대한 자세한 내용은 [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](shortcut-query-files-mds-add-in-for-excel.md)을 참조하세요.  
  
## <a name="data-quality-services"></a>Data Quality Services  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 에는 데이터를 MDS 저장소에 게시하기 전에 일치하는지 확인할 수 있게 해주는 Data Quality Services 기능이 있습니다. 연결을 설정할 때는 DQS 데이터베이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 동일 인스턴스에 MDS 데이터베이스로 설치된 경우 리본 메뉴에 DQS 단추를 표시할 수 있습니다. DQS_Main 데이터베이스가 인스턴스에 없으면 이러한 단추가 표시되지 않으며 데이터 품질 기능을 사용할 수 없습니다.  
  
## <a name="troubleshooting-connections"></a>연결 문제 해결  
 MDS에 연결할 때 모든 문제 참조를 접하는 [ https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx ](https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx) 문제 해결 팁에 대 한 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 대한 연결을 만듭니다.|[MDS 리포지토리에 연결&#40;Excel용 MDS 추가 기능&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|MDS 데이터를 Excel로 로드합니다.|[MDS에서 Excel로 데이터 로드](export-data-to-excel-from-master-data-services.md)|  
|MDS 데이터를 Excel에 로드하기 전에 필터링합니다.|[로드 하기 전 데이터 필터링 &#40;MDS 추가 기능에 Excel 용&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [데이터 로드 &#40;MDS 추가 기능에 Excel 용&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel용 Master Data Services 추가 기능](master-data-services-add-in-for-microsoft-excel.md)  
  
  
