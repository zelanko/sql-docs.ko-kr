---
title: 도메인 관리 작업 종료 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ab6505ad-3090-453b-bb01-58435e7fa7c0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ec0413f72261bf2890c372773a13a662e9182498
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011194"
---
# <a name="end-the-domain-management-activity"></a>도메인 관리 작업 종료
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 도메인 관리 작업 완료, 닫기 또는 취소를 수행하는 방법에 대해 설명합니다. 도메인 관리는 마법사에 의해 수행되지 않으므로 아래 설명된 컨트롤은 도메인 관리 작업의 여러 페이지에서 사용할 수 있습니다.  
  
## <a name="end-domain-management"></a>도메인 관리 종료  
 **마침**  
 도메인 관리를 완료하려면 클릭합니다. 다음 작업을 수행할 수 있는 팝업이 표시됩니다.  
  
-   **예-종료 확인 하 고 기술 자료를 게시**: 현재 사용자나 다른 사용자가 사용할 수 있도록 기술 자료가 게시됩니다. 기술 자료가 잠기지 않고 기술 자료 테이블에서 기술 자료의 상태는 비어 있음으로 설정되며 도메인 관리 및 기술 자료 검색 작업을 둘 다 사용할 수 있습니다. 기술 자료 열기 화면으로 돌아갑니다.  
  
-   **아니요-기술 자료를 종료 한 작업 내용을 저장**: 작업 내용이 저장되고 기술 자료가 잠긴 상태로 유지되며 기술 자료의 상태는 작업 중으로 설정됩니다. 도메인 관리 및 기술 자료 검색 작업을 둘 다 사용할 수 있습니다. 홈 페이지로 돌아갑니다.  
  
-   **취소-현재 화면에 머무르 기**: 팝업이 닫히고 도메인 관리 화면으로 돌아갑니다.  
  
 **취소**  
 작업 내용이 손실되어도 도메인 관리 작업을 종료하고 DQS 홈 페이지로 돌아가려면 클릭합니다.  
  
 **닫기**  
 작업 내용을 저장하고 DQS 홈 페이지로 돌아가려면 클릭합니다. 기술 자료가 잠기며 **기술 자료 열기** 화면의 기술 자료 테이블에서 기술 자료의 상태는 **도메인 관리**가 됩니다. **닫기**를 클릭한 후 기술 자료 검색 작업을 수행하려면 **도메인 관리** 화면으로 돌아가서 **마침**을 클릭한 다음 **예** 를 클릭하여 기술 자료를 게시하거나 **아니요** 를 클릭하여 기술 자료에 대한 작업 내용을 저장하고 끝내야 합니다.  잠긴 기술 자료를 여는 방법은 [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md)를 참조하십시오.  
  
  
