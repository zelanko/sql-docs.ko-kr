---
title: Data Migration Assistant를 사용 하 여 평가 저장 및 로드
description: Data Migration Assistant를 사용 하 여 평가를 저장 하 고 로드 하는 방법을 알아봅니다.
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 995b6b131d9e65ca7a91ce9053583a036fd80fbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75840522"
---
# <a name="save-and-load-assessments-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 평가 저장 및 로드

다음 단계별 지침은 Data Migration Assistant v 5.0 이상을 사용 하 여 데이터베이스 평가를 파일에 저장 한 다음 파일에서 평가를 로드 하는 데 도움이 됩니다.

> [!NOTE]
> 최신 버전의 DMA를 사용 하 여 저장 된 평가를 로드 하는 것 외에도, 사용자는이 기능을 활용 하 여 이전 버전의 Data Migration Assistant에서 사용 하는 json 파일로 내보낸 평가를 로드 하 여 v 5.0 이상에서 결과를 볼 수 있습니다.

## <a name="saving-an-assessment-to-a-file"></a>파일에 평가 저장

1. Data Migration Assistant를 사용 하 여 평가를 실행 한 후 **평가 저장**을 선택 합니다.

   ![평가 저장 대화 상자 열기](../dma/media/dma-save-load-assessments/dma-open-save-dialog.png)

   표준 **저장 ...** 대화 상자가 나타납니다.

   > [!NOTE]
   > Data Migration Assistant에서 평가를 실행 하는 방법에 대 한 자세한 내용은 Data Migration Assistant를 [사용 하 여 SQL Server 마이그레이션 평가 수행](../dma/dma-assesssqlonprem.md)문서를 참조 하세요.

2. 파일의 이름을 지정 하 고 **저장**을 선택 합니다.

   ![평가 파일 이름 지정 및 저장](../dma/media/dma-save-load-assessments/dma-name-save-assessment.png)

## <a name="loading-an-assessment-saved-to-a-file"></a>파일에 저장 된 평가 로드

1. 이전에 파일에 저장 한 평가를 로드 하려면 Data Migration Assistant를 시작 하 고 **모든 평가** 탭에서 **로드 평가**를 선택 합니다.

   ![부하 평가 대화 상자 열기](../dma/media/dma-save-load-assessments/dma-open-load-dialog.png)

2. 로드 하려는 저장 된 평가 파일로 이동 하 여 파일을 선택한 다음 **열기**를 선택 합니다.

   ![평가 파일 열기](../dma/media/dma-save-load-assessments/dma-open-assessment.png)

   로드 한 평가 항목이 **모든 평가** 탭에 나타납니다.

   ![평가 항목 표시](../dma/media/dma-save-load-assessments/dma-display-assessment-entry.png)

3. 평가 항목을 선택 하 고 **평가 열기**를 선택 합니다.

   ![평가 세부 정보 열기](../dma/media/dma-save-load-assessments/dma-open-assessment-detail.png)

   이제 이전에 실행 한 평가의 세부 정보가 표시 Data Migration Assistant.

   ![평가 세부 정보 표시](../dma/media/dma-save-load-assessments/dma-display-assessment-detail.png)
