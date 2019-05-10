---
title: 바로 가기 쿼리 파일(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 11e875d5b171194c3ac8ba4ad33fad51cacacffe
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482666"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>바로 가기 쿼리 파일(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서는 바로 가기 쿼리 파일을 사용하여 자주 사용되는 데이터를 신속하게 연결하고 로드할 수 있습니다. 또한 다른 사용자와 MDS 데이터를 공유할 때에도 이를 사용할 수 있습니다. 워크시트를 저장하고 전자 메일로 전송하는 대신 바로 가기 쿼리 파일을 저장하고 이 파일을 대신 전자 메일로 전송해야 합니다. 이렇게 하면 MDS 저장소에 연결하여 최신 파일을 가져올 수 있습니다.  
  
 바로 가기 쿼리 파일은 다음에 대한 정보가 포함된 XML 파일입니다.  
  
-   MDS 저장소 연결  
  
-   모델, 버전 및 엔터티  
  
-   바로 가기를 만들 때 적용된 모든 필터  
  
-   바로 가기를 만들 때 왼쪽에서 오른쪽으로의 열 순서  
  
 이러한 파일을 목록에 저장하여 추가 기능을 열 때 선택할 수 있습니다. 이를 컴퓨터 또는 공유 위치에 내보내거나 다른 사용자에게 전송할 수 있습니다.  
  
## <a name="queryopener-application"></a>QueryOpener 애플리케이션  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 을 설치한 모든 사용자에게는 QueryOpener라는 응용 프로그램이 설치되어 있습니다. 이 애플리케이션은 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 바로 가기 쿼리 파일을 여는 데 사용됩니다. 바로 가기 쿼리 파일을 두 번 클릭하면 이 애플리케이션이 추가 기능에서 파일을 여는 데 자동으로 사용됩니다.  
  
 이 애플리케이션에서 바로 가기 쿼리 파일을 열면 해당 연결을 "안전한" 연결 즉, 이 위치의 콘텐츠를 신뢰할 수 있는 연결로 지정하라는 메시지가 표시됩니다. 연결을 안전한 연결로 표시할 때마다 연결이 목록에 추가됩니다. 이 목록을 지우려면 **설정** 대화 상자를 열고 **수신 허용 목록에 추가된 서버** 섹션에서 **모두 지우기**를 클릭합니다.  
  
 응용 프로그램에 대 한 기본 위치가 *드라이브*: \Program Files\Microsoft SQL Server\120\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe입니다.  
  
 바로 가기 쿼리 파일을 여는 방법은 두 가지: 가져올 수 있습니다 또는 수 두 번 클릭 하 고 자동으로 열립니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|활성 워크시트의 내용을 바로 가기 쿼리 파일로 저장합니다.|[바로 가기 쿼리 파일 저장&#40;Excel용 MDS 추가 기능&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|활성 워크시트의 내용을 제공하는 바로 가기 쿼리 파일을 전자 메일로 전송합니다.|[바로 가기 쿼리 파일을 메일로 보내기&#40;Excel용 MDS 추가 기능&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [연결&#40;Excel용 MDS 추가 기능&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel용 Master Data Services 추가 기능](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [보안&#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
