---
title: 플랫 파일 대상 구성(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2584cb4a6867d4af3b3f6bc1feff167c900a166d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965616"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>플랫 파일 대상 구성(SQL Server 가져오기 및 내보내기 마법사)
  **플랫 파일 대상 구성** 페이지를 사용하여 대상 플랫 파일의 서식 옵션을 지정하고 계속하기 전에 결과를 미리 볼 수 있습니다.  
  
 이 마법사에 대해 자세히 알아보려면 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조 하세요. 마법사 시작 옵션 및 마법사를 성공적으로 실행 하는 데 필요한 사용 권한에 대 한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 실행](start-the-sql-server-import-and-export-wizard.md)을 참조 하세요.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **원본 플랫 파일**  
 대상 파일의 이름입니다.  
  
 **행 구분 기호**  
 행 구분 기호 목록에서 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**CR**|행이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|행이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|행이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|행이 콜론으로 구분됩니다.|  
|**쉼표로{,}**|행이 쉼표로 구분됩니다.|  
|**탭 {t}**|행이 탭으로 구분됩니다.|  
|**세로 막대 {&#124;}**|행이 세로 막대로 구분됩니다.|  
  
 **열 구분 기호**  
 열 구분 기호 목록에서 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|열이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**CR**|열이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|열이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|열이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|열이 콜론으로 구분됩니다.|  
|**쉼표로{,}**|열이 쉼표로 구분됩니다.|  
|**탭 {t}**|열이 탭으로 구분됩니다.|  
|**세로 막대 {&#124;}**|열이 세로 막대로 구분됩니다.|  
  
 **미리 보기**  
 대상 플랫 파일에 대해 선택한 서식 옵션의 결과를 **데이터 미리 보기** 대화 상자에 표시합니다.  
  
 **변환 편집**  
 **열 매핑** 대화 상자를 사용하여 대상 파일의 행을 삭제 또는 추가하고 열을 구성합니다.  
  
  
