---
title: 버전 정보 설정 및 검색 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8dd7119d66dbd2e904e83d434f1319867b7aa7e7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929204"
---
# <a name="set-and-retrieve-version-information"></a>버전 정보 설정 및 검색
  버전 정보에는 원본 제어 파일의 기록 및 현재 상태가 포함됩니다. 모든 원본 제어 파일에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe는 포괄적인 기록을 유지 관리하므로 시간이 지남에 따라 하나 이상의 파일이 발전하는 상황을 추적할 수 있습니다. 또한 이 정보를 사용하여 모든 파일 버전의 로컬 복사본을 검색하거나 두 개의 파일 버전을 비교할 수 있습니다.  
  
 파일 기록에는 다음이 포함됩니다.  
  
-   동일한 파일의 다른 버전 간에 해당 시퀀스를 식별하는 버전 번호  
  
-   실행된 동작. 파일 작성, 체크 인 및 삭제 작업이 추적됩니다.  
  
-   파일과 연관된 동작을 수행한 사람의 사용자 이름  
  
-   작업이 수행된 날짜와 시간  
  
 또한 Visual SourceSafe는 현재 로드된 솔루션에 대한 현재 상태 정보를 유지 관리합니다. 이 정보는 다음을 비롯하여 현재 파일 상태에 대한 스냅샷을 제공합니다.  
  
-   파일을 체크 아웃한 사용자의 ID  
  
-   선택한 파일의 최신 버전 번호  
  
-   버전을 만든 날짜  
  
-   버전과 연관된 사용자 의견  
  
-   파일을 공유한 프로젝트의 경로  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [파일 기록 보기](../../2014/database-engine/view-file-history.md)  
  
-   [프로젝트 기록 보기](../../2014/database-engine/view-project-history.md)  
  
-   [파일 상태 보기](../../2014/database-engine/view-file-status.md)  
  
-   [파일 검색](../../2014/database-engine/retrieve-files.md)  
  
-   [최신 버전으로 버전 지정](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [파일 비교](../../2014/database-engine/compare-files.md)  
  
-   [파일 공유](../../2014/database-engine/share-files.md)  
  
-   [기록 및 상태 보고서 만들기](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>참고 항목  
 [원본 제어 기본 사항](../../2014/database-engine/source-control-basics.md)  
  
  
