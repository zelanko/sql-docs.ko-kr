---
title: 쿼리 작성기 (보고서 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 358a82555a2f0b3df8a7635cb3ff39a7b09f2e50
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290401"
---
# <a name="query-builder-report-wizard"></a>쿼리 작성기(보고서 마법사)
  쿼리 작성기를 사용하여 보고서에 사용할 결과 집합을 검색하는 쿼리를 지정할 수 있습니다. 다음과 같은 두 개의 쿼리 작성기 중에서 선택할 수 있습니다.  
  
-   쿼리를 지정하고 결과를 보기 위한 매우 단순한 작업 영역을 제공하는 텍스트 기반 쿼리 작성기(기본값). 여러 개의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 사용자 지정 데이터 처리 확장 프로그램에 대한 쿼리 또는 명령 구문, 식으로 지정된 쿼리를 지정할 수 있습니다. 일반 쿼리 작성기는 쿼리를 전처리하지 않고 모든 종류의 쿼리 구문을 포함할 수 있으므로 보고서 디자이너의 기본 쿼리 작성기 도구입니다.  
  
-   보다 뛰어난 화면을 제공하는 그래픽 쿼리 작성기. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 여러 부분에 사용됩니다. 식 또는 여러 부분으로 구성된 SQL 문을 작성하지 않는 경우 그래픽 쿼리 작성기를 사용할 수 있습니다.  
  
     그래픽 쿼리 작성기로 전환하려면 창의 왼쪽 위 모퉁이에 있는 **텍스트로 편집** 단추를 토글합니다.  
  
 또한 다른 보고서에서 쿼리를 가져올 수 있습니다.  
  
## <a name="query-builder-options"></a>쿼리 작성기 옵션  
 **텍스트로 편집**  
 텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너가 모두 쿼리에 대해 작동하는 경우 이 두 디자이너 사이를 전환합니다.  
  
 **가져오기**  
 **쿼리 가져오기** 대화 상자를 열고 사용 가능한 모든 보고서에 대한 .rdl 및 .sql 파일을 표시합니다. 가져온 쿼리를 그대로 사용하거나 쿼리 작성기에서 수정할 수 있습니다.  
  
 **\! (실행)**  
 쿼리를 실행하고 쿼리가 유효한 경우 결과 집합을 반환합니다. 쿼리가 식인 경우에는 실행할 수 없습니다. 식 기반 쿼리인지 확인하려면 보고서 미리 보기를 수행해야 합니다.  
  
 **명령 유형**  
 텍스트, 저장 프로시저 또는 테이블을 직접 지정합니다. 명령 유형의 사용 가능 여부는 지정한 데이터 처리 확장 프로그램에 따라 다릅니다.  
  
 **쿼리 창**  
 쿼리를 입력합니다.  
  
 **결과 창**  
 쿼리에서 반환된 결과 집합을 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [보고서 마법사 도움말](../../2014/reporting-services/report-wizard-help.md)  
  
  
