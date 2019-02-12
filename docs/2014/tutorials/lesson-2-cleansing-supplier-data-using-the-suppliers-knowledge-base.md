---
title: '2단원: Suppliers 기술 자료를 사용 하 여 공급자 데이터 정리 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 42006c68a50497034817cfe8df6c9172ea0cdc3b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036914"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>2단원: 공급자 기술 자료를 사용하여 공급자 데이터 정리
  이 단원에서는 첫 번째 단원에서 만든 **Suppliers** 기술 자료를 사용해서 Excel 파일에서 공급자 데이터를 정리합니다. DQS의 데이터 정리에는 데이터가 기술 자료의 지식을 준수하는 정도를 분석하는 **컴퓨터 기반 프로세스** 및 컴퓨터 기반 프로세스 결과를 검토하고 수정할 수 있게 해주는 **대화형 프로세스** 가 포함됩니다. 데이터 정리 기능은 데이터 원본에 포함된 잘못된 데이터를 식별한 후 잘못된 데이터를 수정하거나 수정을 제안합니다. 또한 도메인 값, 동의어의 선행 값, 도메인 규칙, 용어 기반 관계 및 참조 데이터를 사용해서 고객 데이터를 표준화 및 강화합니다. 컴퓨터 기반 프로세스로 제안된 변경 사항은 대화형으로 승인 또는 거부할 수 있습니다. 자세한 내용은 [데이터 정리](https://msdn.microsoft.com/library/gg524800.aspx) 를 참조하십시오.  
  
 컴퓨터 기반 프로세스에는 DQS 클라이언트 기본 페이지에서 구성 옵션을 사용하여 구성할 수 있는 다음과 같은 임계값이 사용됩니다.  
  
-   **제안 최소 점수:** DQS에서 대체 값을 제안하기 위해 사용되는 최소 점수 또는 신뢰도 수준입니다.  
  
-   **자동 수정 최소 점수:** DQS에서 값을 자동으로 수정하기 위해 사용되는 최소 점수 또는 신뢰도 수준입니다.  
  
 이러한 설정을 구성하는 방법에 대한 자세한 내용은 [정리 및 일치에 대한 임계값 구성](https://msdn.microsoft.com/library/hh510415.aspx) 을 참조하십시오.  
  
 이 단원에서는 Suppliers 기술 자료를 사용해서 입력 데이터를 정리하기 위해 다음과 같은 작업을 수행합니다.  
  
1.  정리를 위한 데이터 품질 프로젝트를 만들고, Excel 파일에서 원본 데이터를 분석 및 정리하기 위해 사용할 기술 자료로 Suppliers 기술 자료를 선택하고, 정리 작업을 선택합니다.  
  
2.  정리할 Excel 열을 기술 자료에서 적합한 DQS 도메인/복합 도메인에 매핑합니다.  
  
3.  컴퓨터 기반 정리 작업을 실행합니다. 컴퓨터 기반 프로세스에서는 Data Quality 클라이언트에 데이터를 대화형으로 정리하기 위해 사용할 수 있는 데이터 품질 정보를 표시합니다.  
  
4.  정리 작업의 결과를 보고 관리합니다. 컴퓨터 기반 프로세스에서 찾은 올바른 값, 잘못되었지만 수정된 값, 변경 값이 제안된 잘못된 값 또는 올바르지 않은 값을 검토할 수 있습니다. 변경 사항을 대화형으로 승인 또는 거부하고, 다음으로 수정 필드를 사용해서 컴퓨터 기반 프로세스의 제안을 수정하거나 재정의할 수 있습니다.  
  
5.  정리 프로세스의 결과를 Excel 파일로 내보냅니다.  
  
6.  새 규칙, 값, 수정 사항 등을 사용 하 여 기술 자료의 지식을 늘릴 수는 도메인으로 정리 프로젝트에서 값을 가져오기...  
  
## <a name="next-step"></a>다음 단계  
 [작업 1: 데이터 품질 프로젝트 만들기](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
