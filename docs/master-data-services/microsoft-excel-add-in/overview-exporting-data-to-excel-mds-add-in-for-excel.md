---
title: '개요: Excel로 데이터 내보내기(Excel용 MDS 추가 기능) | Microsoft Docs'
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 05b5eb61afee1c38c64c2b071efd7b808fade030
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396806"
---
# <a name="overview-exporting-data-to-excel-mds-add-in-for-excel"></a>Overview: Exporting Data to Excel (MDS Add-in for Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 데이터를 사용하려면 먼저 MDS 리포지토리의 데이터를 활성 Excel 워크시트로 내보내야 합니다. 데이터 사용을 마쳤으면 다른 사용자가 공유할 수 있도록 다시 MDS 리포지토리로 가져옵니다.  
  
 내보낼 수 있는 데이터는 액세스 권한이 있는 데이터로 제한됩니다. 데이터 액세스 권한은 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에 설정되거나 프로그래밍 방식으로 설정됩니다.  
  
 많은 데이터를 내보내는 경우 로드 시간이 오래 걸릴 수 있는 데이터를 내보낼 때 표시되는 경고를 설정할 수 있습니다. 이렇게 하려면 **옵션** 그룹에서 **설정**을 클릭합니다. **데이터** 탭에서 **큰 데이터 집합에 대해 필터 경고 표시**를 선택합니다.  
  
> [!WARNING]  
>  MDS 지원 통합 문서는 Excel용 MDS 추가 기능을 사용하여 Excel에서만 열고 업데이트해야 합니다. MDS 지원 통합 문서를 MDS Excel 추가 기능이 설치되지 않은 컴퓨터에서 Excel로 여는 작업은 지원되지 않으며 통합 문서 파일이 손상될 수 있습니다. 데이터를 다른 사람과 공유하려면 워크시트를 저장해서 전자 메일로 보내는 대신 바로 가기 쿼리 파일을 해당 사용자에게 전자 메일로 보내십시오. 쿼리에 대한 자세한 내용은 [바로 가기 쿼리 파일을 메일로 보내기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)를 참조하세요.  
  
## <a name="filtering-data"></a>데이터 필터링  
 다운로드하려는 데이터 양을 제한하려면 내보내기 전에 데이터를 필터링할 수 있습니다. 여기에는 로드하려는 특성(열) 선택, 특성을 표시할 순서 및 사용하려는 멤버(데이터 행)이 포함됩니다. 자세한 내용은 [내보내기 전 데이터 필터링&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)을 클릭합니다.  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>자동으로 연결 및 자주 사용되는 데이터 로드  
 항상 동일한 서버에 연결하고 동일한 데이터 집합을 내보내려는 경우 연결 및 필터 정보를 포함하는 바로 가기 쿼리 파일을 만들 수 있습니다. 쿼리 파일에 대한 자세한 내용은 [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)을 클릭합니다.  
  
## <a name="refreshing-data"></a>데이터 새로 고침  
 내보낸 후 다른 사용자가 MDS 리포지토리의 데이터를 업데이트할 수 있습니다. MDS 이외의 데이터에 대해 변경한 내용을 손실하지 않고 이 데이터를 검색할 수 있습니다. 자세한 내용은 [데이터 새로 고침&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|MDS 데이터를 Excel에 로드하기 전에 필터링합니다.|[내보내기 전 데이터 필터링&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
|MDS 데이터를 Excel로 로드합니다.|[Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|데이터를 다운로드하기 전에 열 순서를 변경합니다.|[열 순서 바꾸기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [연결&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel용 Master Data Services 추가 기능](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [보안&#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
